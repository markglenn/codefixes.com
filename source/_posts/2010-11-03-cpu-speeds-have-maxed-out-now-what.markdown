---
author: markglenn
layout: post
title: CPU speeds have maxed out... now what?
description: Using multiprocessing now that CPU speeds have maxed out
keywords: CPU,multicore,programming,ARM,RISC,thread,parallel,LINQ
comments: true
categories:
- Programming
---

So, you now have this 8 core powerhouse. It has more horsepower than your old
Mustang, but your code is only using 1/8th of that power. How come? Because
while the rules of Moore's law changed, your code hasn't.

<!--more-->

The problem isn't that technology is changing, it's that your language isn't
changing quick enough. Threads are the answer, or they were.  Threads were the
answer a few years back when we had two cores, maybe four. Now we have eight
with sixteen just around the corner. And worse yet, cores may become less
powerful to reduce heat and power.
[ARM](http://en.wikipedia.org/wiki/Arm_architecture) processors have moved on
to the [personal computer](http://en.wikipedia.org/wiki/Netbook) and don't seem
to be [slowing down](http://simmtester.com/page/news/shownews.asp?num=13364).
ARMs are a form of
[RISC](http://en.wikipedia.org/wiki/Reduced_instruction_set_computer) processor
or "Reduced Instruction Set Computer." This means that it has a smaller
instruction set than the laptop you have now. An instruction that takes one
tick may take two in the future. 

Okay, what gives? Why go backwards? Because it's smaller, more efficient, less
power hungry, etc... Smack a few dozen of those cores together and you have one
fast machine. Now, I can't predict the future obviously, nor am I marking the
future death of the x86 instruction set. I'm just pointing out one possibility
to show my point. 

Okay, what is my point? You're coding style will have to change if you want to
stay "future proof." [Threading is difficult](http://blogs.msdn.com/b/jmstall/archive/2008/01/30/why-threading-is-hard.aspx).
It's error prone, hard to predict, even harder to optimize. And what do you get
out of this headache? Code that still takes only 1/8th of the CPU power
available to it. The problem is, most of the time your code is waiting for
input, an event to fire, or some I/O process to complete.  You have to manage
separate threads just to do the same job that was done on DOS years ago. Users
expect responsive applications. If you want the truth, try using iTunes on a
Windows PC.

So some languages have added features to help with calm your worried mind. For
example, .NET added [Parallel Extensions](http://en.wikipedia.org/wiki/Parallel_Extensions) 
and the [Reactive Extensions (Rx)](http://msdn.microsoft.com/en-us/devlabs/ee794896.aspx). And
C++ finally added [lambda expressions](http://en.wikipedia.org/wiki/C++0x#Lambda_functions_and_expressions)
to the mix (although it was [available in boost](http://www.boost.org/doc/libs/1_44_0/doc/html/lambda.html) for a while).
These help reduce the noise of making your code threaded, but still miss out
when it comes to [thread safety](http://en.wikipedia.org/wiki/Thread_safety),
[deadlocks](http://en.wikipedia.org/wiki/Deadlock), or
[starvation](http://en.wikipedia.org/wiki/Dining_philosophers_problem).

You probably know the answer already. People have been blogging about it for a
while now. It's the new kid on the block... er, well, old kid.  It's
[functional programming](http://en.wikipedia.org/wiki/Functional_programming),
based off of [lambda calculus](http://en.wikipedia.org/wiki/Lambda_calculus)
from the 1930s. You may hear it by other names, such as F\#, Haskell, Scheme,
Erlang, OCaml, or LINQ. 

Wait, LINQ? Yeah, you've been using functional programming all this time. All
those lambdas you've been throwing at LINQ are examples of functional
programming. And if you've done it correctly, they are possibly examples of
*purely functional programming*. Those lambdas don't have any side effects, so
a search can be run on that list of 10,000 items on all of your cores, and
without any work on your part. Parallel Extensions in .NET 4.0 does all the
heavy lifting for you. This is great news, you say... 

But alas, it's not the final chapter in this story. Parallel Extensions are
great if you constantly have to search for something in a list of 10,000 items,
but your code answers to clicks and I/O events. You have more important things
to do than playing around with something that's of little to no use to the
general coding population, building client applications. What we need is a true
functional language. 

And this is where the story ends, for now. Functional programming is the next
logical step. Just imagine a language where you can write all methods, and they
would magically run on other threads when branching, and that they would join
up again when the branches merge. The code could trigger a UI update from one
thread and not care if it's on the UI thread or not. No longer are these your
problems. You now write functions with no side effects; functions that are
[idempotent](http://en.wikipedia.org/wiki/Idempotence). Let the compiler worry
about where the code should run, you have more important things to do. 

It has started. Take a look at [node.js](http://nodejs.org/). They use event
driven functions. Most of the time, these functions call out to node.js,
requesting or sending data, and send a callback to be called when it completes.
No waiting.  The server happily handles the I/O in the background and can
process other requests while that Ruby on Rails site just sits there. It's
pretty neat stuff. 

You can have this too for your desktop applications.
[F\#](http://research.microsoft.com/en-us/um/cambridge/projects/fsharp/default.aspx)
brings .NET to the functional world. [Qt](http://qt.nokia.com/) has
[qtHaskell](http://qthaskell.berlios.de/).
[wxWidgets](http://www.wxwidgets.org/) has 
[wx and Erlang](http://www.erlang.org/doc/apps/wx/chapter.html). That means you can
write WPF/Qt/wxWidgets applications that handle everything with event driven
code and purely functional calls. It's available now.

Problem is, functional programming is also hard, but in a different way.  Of
course, that's for another place and time. For now, pick up a copy of 
[Real World Haskell](http://www.amazon.com/gp/product/0596514980?ie=UTF8&tag=codefixes-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0596514980)![image](http://www.assoc-amazon.com/e/ir?t=codefixes-20&l=as2&o=1&a=0596514980)
or [Real World Functional Programming: With Examples in F\# and C\#](http://www.amazon.com/gp/product/1933988924?ie=UTF8&tag=codefixes-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=1933988924)![image](http://www.assoc-amazon.com/e/ir?t=codefixes-20&l=as2&o=1&a=1933988924)
and start coding.
