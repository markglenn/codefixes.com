---
layout: post
title: "Think Functional: Definition of Idempotence"
date: 2013-08-31 16:16
comments: true
categories: 
---
In the most basic of terms, idempotence pertains to the property of certain functions to be applied more than once and always
returning the same result.  While originally a mathematical term, it has since been added into the vocabulary of the computer 
science world.  It has been used from discussing the basic paradigm of functional programming, to databases, to web
development.  It has such a wide range of uses, its surprising to me that I only in the past few years started really knowing
what it means.  Let's step back and really think about the tenets of idempotence and what it means to the programmers
of the world.

<!-- more -->

The definition of idempontence varies based on context.  However, stating a function (whether it is a RESTful call,
function call, or SQL command) is idempontent usually means that function has the following properties:

1. The function should be referentially transparent.
2. The function should be reentrant.
3. The function should not have any side effects.

That's the basic definition I could find on Wikipedia, but it makes it sound much more complicated than it really needs to
be.  This may be because the principles of Computer Science are so intertwined with mathematics that we like to discuss
these ideas using equations and complex terminology.  However, the idea of idempotence is easy enough to grasp for 
mathematics laymen such as myself.

The function should be referentially transparent
------------------------------------------------

Referential transparency of a function suggests that a function call can be replaced with a hardcoded result value without
changing the behavior of the program.  For example, let's say we have a method that calculates the area of a rectangle.
Simple enough to build this using ruby.

``` ruby
# Calculate the area of a rectangle
def area( x, y )
  x * y
end

# Call the area method
my_area = area( 10, 20 )

puts my_area # 200
```

As you can see, a simple call to the area method with x equal to 10 and y equal to 20 will return a result of 200.
We can also see that if we call `area( 10, 20 )` any amount of times, it will always return that same result.  Knowing
this, we can easily enough replace all that code with this:

``` ruby
# Calculate the area of a rectangle
# def area( x, y )
#   x * y
# end

# Call the area method
# my_area = area( 10, 20 )
my_area = 200

puts my_area # 200
```

Haskell, a functional programming language, has this type of replacement built in since it's built on the idea that a
function should have referential transparency.

``` hs
let area :: Int -> Int -> Int
    area 10 20 = 200
    area x y = x * y

show( area 10 20 ) -- "200"
```

As we can see here, when we call `area 10 20` it runs the first method that returns the hard coded value of 200.
Any other values will run the second version of the function.

The function should be reentrant
--------------------------------

A function is considered reentrant if it can be safely interrupted while in the middle of running and re-executed
before the first pass is completed.  This can happen on a multitasking operating system, which is pretty much every
O/S in existence today.  For example, let's say we have two threads running the same method on a single core machine.
At any time, the operating system can stop the first thread and start running the second.  In the case that the two
threads are executing the same method, the two threads should not clash.  No shared data should be modified that could
cause the first thread to be in an unknown state when it continues executing.  Let's look at an example of a 
non-reentrant function

``` ruby
string_value = ""

def add_to_string( line )
  string_value += line

  # Thread interrupted here

  string_value += "\n"
end

thread1 = Thread.new{ add_to_string( 'line1' ) }
thread2 = Thread.new{ add_to_string( 'line2' ) }

thread1.join
thread2.join

puts string_value # "line1line2\n\n"
```

As you can see, calling add_to_string on two different threads can cause an unknown state if the method is swapped out
in the middle of execution.  While we'd expect `line1` and `line2` to be on separate lines, they come out on one.  This
method is considered non-reentrant because it modifies a global state, in this case `string_value`.

Now, you may believe that reentrant and thread safe are synonymous, but they are different in a very important way.  Let's say
we modified this code to read as the following:

``` ruby
mutex = Mutex.new
string_value = ""

def add_to_string( line )
  mutex.synchronize do
    string_value += line
    string_value += "\n"
  end
end

thread1 = Thread.new{ add_to_string( 'line1' ) }
thread2 = Thread.new{ add_to_string( 'line2' ) }

thread1.join
thread2.join

puts string_value # "line1\nline2\n"
```

This method is clearly thread safe, but it no longer is reentrant.  When `thread2` decides to jump in and run `add_to_string`,
it can't since `thread1` holds a lock.  It must wait until `thread1` is complete before running.  It cannot reenter the method.
Instead, we can just pass in all state, including `string_value` to overcome this.

``` ruby
def add_to_string( original, line )
  original += line
  original += "\n"

  original
end
```

This way the method is not only thread safe, but also reentrant.  It does not rely on any outside scope to execute.  The 
method can be stopped in the middle of execution and recalled on a different thread without side effects.

The function should not have any side effects
---------------------------------------------

Speaking of side effects, that is probably the most important aspect of idempotence.  The method should not have any side effects.
What this means is that every piece of data outside of the method should remain pristine when running a method.  It cannot change
any values passed in, any values outside of its own scope, or make any changes in the operating system.  Forget when you learned what
a function was in computer science and go back to your algebra days.  If your algebra teacher showed you the function `x = x + 1`, you
would have told her she was crazy since this doesn't make any sense.

When it comes down to idempontent methods, this also remains true.  A function in algebra is denoted as `f(x) = ...`.  It takes in one
or more inputs and returns a result from just those inputs.  Think about your code in the same way.  If I passed in values to your 
function, I expect calculations to be done only on those values.  It shouldn't change the global variable, `num_calls`.  It shouldn't
create any files.  It shouldn't change the state of any value outside of the function.  When I call your function, I expect nothing to
change.  I only expect a return value.

Now, to play devil's advocate, there is always some side effect of calling a method.  That side effect is the time taken to execute
the code.  Most of the time, this can be safely ignored.  There is always an opportunity cost to running code, so we can't change
that even if we wanted to.

More Information
----------------

I've talked previously about idempotence.  If you want to learn more about the "why" of idempotent functions, please check 
out the following articles and expect some further discussions:

* [Think Functional: Immutable Types and Idempotence](http://www.codefixes.com/2010/11/think-functional-immutable-types-and-idempotence/)
* [Think Functional: Lambdas and LINQ](http://www.codefixes.com/2010/11/think-functional-lambdas-and-linq/)
