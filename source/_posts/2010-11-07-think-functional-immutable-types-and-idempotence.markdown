---
author: markglenn
layout: post
title: "Think Functional: Immutable Types and Idempotence"
description: Programming using immutable types and idempotence
keywords: think functional,functional,programming,erlang,haskell,c#
comments: true
categories:
- .NET
- C++
- Programming
---

I already talked about functional programming recently in a 
[prior article](http://www.codefixes.com/2010/11/cpu-speeds-have-maxed-out-now-what/),
however I state that functional programming is difficult (but in a
different way). The problem is it looks like you have to forget
everything you learned about object oriented and procedural programming.
Seems like a waste to throw away all that good knowledge to blindly go
down a path that hasn't even hit mainstream yet. You don't have to. You
can start programming "functionally" right now no matter what language
you use.

<!--more-->

Functional programming doesn't require esoteric languages. It's
more of a mind set than anything. Sure you could go right now and
download [Erlang](http://www.erlang.org/) or
[Haskell](http://www.haskell.org/), but I can tell you that you're about
to go down a long, difficult road. The problem is you not only have to
learn a new language, but you still need to learn functional
programming. Instead, I'll be writing a series of articles on how to
implement functional ideas in your current language.

So, where do we begin? Probably the first idea to learn is about 
[immutable objects](http://en.wikipedia.org/wiki/Immutable_object). The general
idea is that once an object is created, it can never be changed. Let
that sink in for a second. If you have never created immutable types
before, this may seem strange. In C\#, for example, you can see a few
areas where immutable types are present. Take the C\# string type. Once
you create a string, it can never be changed. All the methods return a
new string with whatever changes you made. 

``` csharp
string hello = "hello";
string world = "world";
string helloWorld = string.Join( " ", new[ ] { hello, world } );
```
In the prior
example, both strings "hello" and "world" are unchanged by any methods.
You *can* set a reference to a new reference with different data, but
the original data will remain unchanged until its garbage collected. The
benefit here is that we now have a strict rule we can leverage when it
comes to threading. Because the object can never change, there won't be
any issues with thread safety. If two threads try to access that same
reference, no big deal. There will be no concern of one thread changing
the data from under the nose of the other. 

So, how do we define an
immutable type? This is where things get a little hazy. There are no
strict rules that governs immutability in many object oriented
languages. In C\#, we can create class members that are
[readonly](http://msdn.microsoft.com/en-us/library/acdd6hb7\(v=VS.100\).aspx).
This allows the data to be set within the constructors only, and then be
set in stone. 

``` csharp
public class ImmutableClass 
{ 
	private readonly int val;

	public int Val 
	{ 
		get { return val; }
	} 
	
	public ImmutableClass( int value )
	{ 
		this.val = value;
	}
}
```

In C++, we don't have that option because there's no such thing as the readonly
type. In that case, we need to create class methods that are
[idempotent](http://en.wikipedia.org/wiki/Idempotence). Idempotent means
that the method has no side effects, however, what does that really
mean? My understanding of this is that the code will not make any
changes to any existing data or interface. It won't change any
pre-existing data. It also won't make any calls outside that may make a
change, such as doing any input or output. Basically, if you call a
method, the output will be exactly the same if you call it again with
the same parameters. In other words, the code has "no side effects." If
all your methods are like this, you all of a sudden have an immutable
type. 

In C++, this is done by adding the **const** keyword to the end of methods. 

``` cpp
int ExampleClass::Multiply() const
{ 
	return this->value1 * this->value2; 
}
```

This isn't a C++ only idea,
however, other languages may not have the same keyword. The idea to take
from this is to create classes that follow these rules. You don't
specifically need the compiler to force these rules for you, although it
does help. That's where functional languages come into play. They will
force these rules on your code for you.

Now you have an understanding of
the basic rules behind functional programming. Next time we'll go into
more of the ideas on using idempotent methods in real world ways. We'll
also discuss how you can actually connect these "functional" methods to
standard methods.
