---
layout: post
title: "Becoming Great"
date: 2012-01-17 16:31
comments: true
categories: 
---
As software developers or engineers, we are constantly on the prowl to improve our development and design skills.
There are thousands of books, countless blogs, and over 1400 languages (based on the results seen at
[99 Bottles of Beer](http://99-bottles-of-beer.net/)).  There are only 24 hours in a day and most of it is spent
working, sleeping, commuting; just living our lives.  Who really has the time to keep up with how quickly technology
is moving?  It's just not humanly possible.  We have to stop trying to become experts and start becoming _good enough_.
This is when we will truly become great.

<!-- more -->

This goes against everything I was taught growing up.  I was always told that to be the best, you had to force yourself
to become that expert.  The problem lies in that technology has advanced to such a degree that it's not possible to 
become that expert in a short enough time period to even stay relevant.  No time in history has there ever been such
a growth in a field that one could obsolete him or herself so quickly just by trying to learn everything there
is to know about their profession.

Take programming methodologies as an example.  If you know assembly, you will know that there is no such thing as a loop.
Sure, you have things such as JNZ (Jump if Not Zero) or any of the other conditional jump statements, but those are just
gotos with a condition attached to them.  This was and is still common when you jump down to most byte code.  For and
while loops just don't exist in these contexts.  All of a sudden, with an influx of procedural languages, and with an 
article written by Edsger W. Dijkstra named 
[Go To Statement Considered Harmful](http://www.u.arizona.edu/~rubinson/copyright_violations/Go_To_Considered_Harmful.html), 
this was bad practice and programmers had to adapt by using loops, method calls, etc.

The same happened with object oriented programming, following procedural.  The use of functions alone was deemed bad
practice, so most of us moved on to thinking in objects, interfaces, and methods.  It's happening again today with
functional languages such as Erlang and Haskell.  Again, object oriented programming is considered harmful because
it has too many side effects.  So, some people are moving on.  This is not going to stop any time soon.  The explosion
in computing power has had the effect of exploding the lines of code required based on what users expect in their 
software.  New methodologies have to be created to mitigate some of these issues as they arise.  

This doesn't even go into the vast number of programming languages in production today.  Take in all the legacy code
still written in languages such as Cobol and add in languages such as Ruby, C++, Python, etc.  Then you add in the 
managed languages such as those written for the .NET framework and the Java Runtime Environment (JRE).  Finally add in
some of the newly popular languages such as Erlang and Haskell.  What you get is the impossible task for any person
to keep up with the technology.

So How Do I Keep Up?
====================

This is an interesting dilemma.  On one hand, I spent the first part of this post explaining that you can't keep up,
but now I'm going to explain how you can.  I consider myself lucky.  I've had the opportunity to work in a huge range
of industries on a large number of languages.  In college, I was a C++ guy.  Growing up, I spent years honing my
skills in its idiosyncrasies.  And then, when I graduated and need a job, I took on C#.  My next job went back to C++
but mixed in some Perl and Python, I then went back to a mix of C++ and C#.  Finally, I switched completely over to
Ruby and Rails.  This makes me fairly marketable since I can confidently apply for a job in C++, C#, Ruby, Python, 
or Perl.  Being marketable should be high on anyone's priorities due to the state of the job market in a whole 
(recession) and the job market for programmers (booming).  

Now I'll tell you what I'm not.  I don't have any certifications.  I've never been comfortable enough with a 
language to contribute to their core library.  I don't know exactly how the garbage collectors work in .NET or
Java.  There are a lot of things I just don't know about the languages I work in daily, the small details about
a language that are not required to be known to write great code within its confines.

Even though I can't call myself an expert at any of these languages, I can say that I'm a jack of all trades.  I 
decided early in my career that I would not focus solely on one language because they can go out of popularity
multiple times in my lifetime.  I've shown instead that I can adapt to change in infrastructures.

It's not a difficult task.  On the contrary, it's quite easy.  Instead of continuing to read the same blogs on only
Ruby, branch out and start reading about .NET or Java.  Get a better understanding of what the alternatives are, 
and maybe one day you'll find that the language you know and love just may not be the perfect solution for your
next project.

Master of None
==============

When people say "Jack of all trades," we all know the next line to that statement is "master of none."  This can be 
worrisome to quite a few people because they believe that will hinder their career growth.  If you look at job 
descriptions for senior level developers, you'll see things such as "requires 5+ years developing in X," or "looking 
for an expert in Y."  If you looked at my resume, that would have made me unqualified at my current job because
I never had written a line of production ruby code in my life before it.  On the coding test, I had to look up
half of the ruby methods because they weren't ingrained into my brain yet.  Of course, I did get the job 
despite these shortcomings due to my broad knowledge of programming.

Theres another side effect of broadening your knowledge.  You will get a different perspective on the problems
you encounter in your job.  Learning functional programming will teach you how to handle threaded applications
simpler in C# or Java.  Learning a static language will give you a better understanding of what strict types
gives you in Ruby.  You will be able to know when it's best to use TCP to send messages to another process and
when it's better to use a message queue.  

While you may not know exactly how to install and instantiate the message queue, you will find it much easier 
to learn how to do it.  You have been practicing learning new tools, so you will be able to pick up basics of
setting up [RabbitMQ](http://www.rabbitmq.com/) knowing right away that it uses Erlang's cookie system for security.
Once you break free of trying to become an expert will you finally start becoming great.
