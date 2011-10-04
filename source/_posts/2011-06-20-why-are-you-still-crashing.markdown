---
author: markglenn
layout: post
status: publish
title: Why are you still crashing?
comments: true
keywords: programming,.NET,crash,bug
description: You can avoid crashes in your application
categories:
- General
- Programming
---

{% img right /images/blog/error2.jpg "Windows Error" %}
I know this is going to be a bit of a controversial topic, but this has
come to bite me recently. An application that I recently purchased that
allowed me to access [GitHub](https://github.com/markglenn) from my
iPhone now crashes every time I start it up due to GitHub updating their
API. I don't mean it shows an error message, but crashes back to the
home screen. Obviously this is a major annoyance to anyone trying to use
the app as seen by the recent negative reviews it has been receiving. Of
course, the update to fix the bug was sent to Apple within the same day,
but we all know how fast Apple can be with their review process.

<!--more-->

What happened is GitHub changed the string format of dates within their
API. This is obviously what we call a "breaking change," and their API
probably should have been versioned to avoid these types of problems.
However, that's not the real issue that I'm trying to address. The
problem is the application didn't safe guard how they access the API.
The assumption was that GitHub wouldn't change their API in any way that
would break compatibility. I question why you would assume anything when
it comes to programs.

## Why aren't you handling errors?

This is the most obvious issue. I remember back a few years back when
writing C/C++ applications for embedded hardware that if we didn't
handle an error, you would get random behavior. We didn't have stack
traces, core dumps, or even printfs (We had a pretty primitive hardware
setup since we were R&D). What we did instead was check every return
value and used interrupt handlers to handle the *exceptional* cases. In
other words, we used all the tools available to us to make sure we
didn't fail. In embedded systems, we truly had exceptional cases such as
blown parts, power surges, and even dropped prototypes. String parsing
errors are nothing compared to random hardware failures.

One thing that was drilled into my skull over and over again was that
you need to handle every error state. If a method returned a value and
you ignored it, you would be reprimanded. If a function returned a
value, the function's author obviously believed it was important enough
information to include. You need to check it. With C, there were no
exceptions, so an ignored error caused undefined behavior.

## Why are you ignoring your exceptions?

This is even more important, and arguably easier to handle, with
languages that support exceptions. Instead of checking the return value
of every function call or checking the global error value, you can check
for errors on an entire block. The call stack is unwound to whichever
position you want that can successfully handle the exception.

Heck, even having a catch all handler at the root of your application
that just shows an error message then quit would be better than letting
an exception unwind the entire stack of your application to be handled
by the operating system. Then I would know that an exceptional situation
occurred instead of thinking the program was just poorly coded.

## Why are you still using a non managed language?

Okay, this one may seem odd and controversial , especially since all my
examples so far are about embedded C and an iPhone application. This
obviously doesn't relate to certain types of programs that require high
performance (games, trading applications, etc.) or that have the
requirement of a certain language (embedded software). For the rest of
the situations, a language should be used that can help write better,
safer code. There really is no reason to still use C/C++ or Objective C
now that there are multiple options.

Yes, Objective C is questionable since Apple puts this requirement on
all Cocoa applications, but
[MonoMac](http://www.mono-project.com/MonoMac) and
[MonoTouch](http://monotouch.net/) are great solutions which use a .NET
runtime or compiler. MonoTouch does cost money on top of the money you
have to shell out to Apple for the opportunity to write iOS
applications, so your mileage may vary. I also know Adobe has a similar
solution and I wouldn't be surprised if Java had something also.

The real benefit is garbage collection. Why manage your own memory if
you don't have to? Memory management is difficult to handle perfectly,
especially with exceptions. Patterns such as
[RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization)
in C++ and [smart pointers](http://en.wikipedia.org/wiki/Smart_pointer)
mitigate these worries, but the language still allows you to shoot
yourself in the foot if you aren't careful with using these. I hear
[iOS 5](http://developer.apple.com/technologies/ios5/) is going to get
[reference counting](http://en.wikipedia.org/wiki/Reference_counting)
for Objective C, so this may be a moot point in a few months.

## Patches are not a solution

Sure, patches for the problem are good. We need fixes so we can run your
software, but that is not the end solution. It is only a bandage on an
incomplete design. What you need to add with the fix is error checking
to make sure this never happens again. Don't just fix whatever error
you're getting. Make sure that all possible future errors are handled.

## We are all human

Now this may come off as a rant, but I know we're all human. I've
definitely had crashes in programs that I've written. Errors happen that
sometimes we really can't predict. However, the options listed above
should help mitigate some of the most likely situations. Just remember
that while we are all human, we can still avoid the crash situation.
Error messages, no matter how cryptic, are infinitely better than core
dumps alone.
