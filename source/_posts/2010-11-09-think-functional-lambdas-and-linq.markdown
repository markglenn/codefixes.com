---
author: markglenn
layout: post
slug: think-functional-lambdas-and-linq
status: publish
title: 'Think Functional: Lambdas and LINQ'
categories:
- .NET
- Programming
tags:
- c#
- functional
- LINQ
- programming
---

If you haven't read the previous post, 
[Immutable Types and Idempotence](http://www.codefixes.com/2010/11/think-functional-immutable-types-and-idempotence/),
I recommend doing so now. It will help you get a better understanding of
what I'll be talking about here. Now that we have basic knowledge of
*what* a pure method really is, we need to figure out how to use it.
It's not that difficult, but the syntax may require some getting used
to. We'll be using .NET's LINQ component to describe how to use lambdas
to increase your code efficiencies, but these ideas travel well into the
C++ world using either
[Boost.Lambda](http://www.boost.org/doc/libs/1_44_0/doc/html/lambda.html)
or
[C++0x](http://en.wikipedia.org/wiki/C++0x#Lambda_functions_and_expressions),
if your compiler supports it.

<!--more-->

As we recall, we were creating idempotent
(pure) methods and forcing the rules by using immutable objects. We can
easily use these ideas to create queries and projections directly in
code, where the original data is not modified. The benefit here, again,
is that this will scale. Also, as will see soon, the application will
run faster by the magic of 
[lazy evaluation](http://en.wikipedia.org/wiki/Lazy_evaluation).

For example, let us say we have a list of ten thousand orders.

``` csharp
// Load all the orders IEnumerable<Order> orders = OrderRepository.GetAllOrders( );
```

Notice that the result returned
is a generic IEnumerable. What happens here is that GetAllOrders doesn't
necessarily need to return the full list of orders, it can skip this
step and return the *intent* of getting the full list of orders. The
IEnumerable is actually hiding what the GetAllOrders method is really
returning, an
[IQueryable](http://msdn.microsoft.com/en-us/library/system.linq.iqueryable.aspx).

``` csharp
public static class OrderRepository
{ 
    public static IQueryable<Order> GetAllOrders( )
    {
        return orders.AsQueryable( );
    }
}
```

The IQueryable interface provides a decoupling of the query
source from the logic to be run upon it. In other words, the IQueryable
interface stores the methods (lambdas) to be called upon its source in a
tree structure. Later, when you want to iterate over the list, it will
run the commands live on the data. This can significantly reduce the
amount of data returned and won't force you to create multiple lists of
the same data in the various steps of the query. Haskell takes this one
step further and actually allows infinite lists. This may seem odd to
you, but since everything is lazily loaded, the list doesn't need to
actually exist in memory.

``` hs
take 5 [1..]
[1,2,3,4,5]
```

Also, the IQueryable defines an immutable type, so
it may be able to run on multiple cores. This is not always the case,
though. For example, an IQueryable can be attached to a database, and
therefore only run one SQL command. For now, let's assume the list is
stored in a randomly accessible location such as in memory.

What we can
do with these queryable objects is throw expressions or lambdas at them.
The IQueryable interface defines a long list of methods that can be
executed, such as Where, Select, FirstOrDefault, etc. Each of these
methods take in a lambda and will run that anonymous method against the
function. For example, if we wanted to reduce our list of orders down to
only the ones that were over $1000, we could do the following.

Lambdas in C\# use a new operator that looks like an arrow (=\>). This may be
confusing at first, but generally becomes easier to comprehend as time
goes on. I find it easier to talk the expression out loud and replace
"=\>" with "such that." In the following example, I would say "Expensive
orders = orders where 'o' such that 'o' dot total price is greater than
one thousand." If you can speak it out loud, it will be easier to
understand. Of course, lambdas go deeper than this example, but you can
find many [other examples of the syntax](http://msdn.microsoft.com/en-us/library/bb397687.aspx) by
searching the web.

``` csharp
var orders = OrderRepository.GetAllOrders( );
var expensiveOrders = orders.Where( o =\> o.TotalPrice \> 1000.0M );
```

As I said before, the IQueryable
is considered an immutable type. It will return a new query object every
time you add more expressions to it. In this case, we now have a new
query stored in expensiveOrders. The query stores a series of
expressions for later use, allowing it to be lazily invoked. This can
save us a tremendous amount of CPU work. If we did the above using a
simple foreach loop, it may take a long time to run through all of them.

``` csharp
var expensiveOrders = new List<Order>( );

foreach( var order in orders)
{ 
    if( order.TotalPrice > 1000.0M )
        expensiveOrders.Add( order );
}
```

In this case, the program would
be forced to loop through every order, even though they may not be all
used. In a user interface, you can't possibly show all the results of
this query on the screen simultaneously. It could require many greater
magnitudes of view space than the screen offers. We would need to
display the list in pages. Of course, in the previous example, even
though we may only show ten results, all ten thousand original orders
would need to be checked.

However, if we stuck with LINQ, the query
won't be run until it is finally forced.

``` csharp
int pageSize = 10;
int page = 0;

// Query first created
var orders = OrderRepository.GetAllOrders( );

// Not run yet
var expensiveOrders = orders.Where( o => o.TotalPrice > 1000.0M );

// Still not run
var displayedOrders = expensiveOrders
    .Skip( page * pageSize )
    .Take( pageSize );
    
// Now the query is finally run
foreach( var order in displayedOrders )
    DisplayOrder( order );
```
Although it's not quickly apparent, the query is finally run before being passed to
DisplayOrders. In this case, only ten results are needed. Because of the
use of LINQ, the query will be stopped short once ten items are taken
from the results. 

Now that we know about pure methods and lazy
invocation, let's use that knowledge to actually build faster code. Next
time, we'll take a look at
[PLINQ](http://en.wikipedia.org/wiki/Parallel_Extensions#Parallel_LINQ)
and the [Parallel Extensions](http://en.wikipedia.org/wiki/Parallel_Extensions) library.
