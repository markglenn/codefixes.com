---
author: markglenn
date: '2011-09-19 21:53:12'
layout: post
slug: cross-platform-net
status: publish
title: Cross Platform .NET
comments: true
categories:
- .NET
- Programming
tags:
- c#
- programming
- ui
---

[{% img right /images/blog/Mono-gorilla-aqua.100px.png %}](http://www.mono-project.com/Main_Page)
Working on software that runs on multiple machines can be time consuming, error
prone, and complicated. Not only do each of the three major operating
systems have different style guidelines, but they even have different
standard programming languages. Mac OS X has [Objective C](http://en.wikipedia.org/wiki/Objective-C) and
[Cocoa](http://cocoadevcentral.com/), Windows has
[.NET](http://en.wikipedia.org/wiki/.NET_Framework) and
[WPF](http://msdn.microsoft.com/en-us/library/ms754130.aspx), and Linux
has C/C++ and [GTK+](http://www.gtk.org/) or [KDE](http://www.kde.org/).
No wonder cross platform applications look so out of place. However, as
unlikely as it may seem, .NET may be the best solution to the native
looking cross platform problem.

<!--more-->

## Java, what could have been

Java was supposed to be the solution to making your applications work
across multiple platforms. While the 
"[write once, run anywhere](http://en.wikipedia.org/wiki/Write_once,_run_anywhere)" slogan
is quite accurate, you can easily pick out a java application on every
desktop platform. Java currently uses its own UI framework named Swing.
The problem is that to make sure that applications run properly on all
the platforms, swing does not follow any of the UI standards set by
Windows, Mac OS X, GTK, or KDE. It also does its own software based
drawing of all its widgets. Because of this, Java has gotten a
reputation for being slow and laggy. The language is quite fast, keeping
up with .NET and in a close race with C/C++, but the UI has really held
it back.

## Qt, the C++ solution

The [Qt framework](http://qt.nokia.com/), by Nokia (previously
Trolltech), is an impressive cross platform C++ framework that tries to
solve some of the same things Java set out to do, but using the tried
and true C++ language. I've used Qt since somewhere around version 2,
and I've found that for a C++ developer, Qt is quote an impressive
framework. Nokia has also put together an IDE specifically for Qt which
inclues code completion which has been difficult in the past due to Qt's
precompiler.

Also, Qt is another framework that does its own widget
drawing, but has the added benefit of supporting hardware acceleration.
This makes Qt's widget drawing to be as fast or faster than native
widgets. If you don't use the hardware acceleration for whatever reason,
the Qt "trolls" have optimized the heck out of their drawing code. They
also have different skins for the different operating systems to make
the widgets look native, however don't expect all widgets to be there or
look 100% the same. All in all, if you know and like C++, Qt may be a
decent solution.

One of the problems with Qt is that it's built on C++.
While I'm a C++ fan, the development time for anything is dramatically
increased. C++ is verbose in general because of the header/source files,
sometimes making it feel like you are writing twice the amount of code.
C++ compilers are also slow due to complicated syntax rules and 
[C++ template generation](http://stackoverflow.com/questions/3634203/why-are-templates-so-slow-to-compile).
This makes development slow compared to some of the snappier compilers
for other languages. You also have to take into account compiling a
different executable on every platform. Since the executable code is not
run within a virtual machine, it needs to take into account the
differences between platforms itself.


## Mono and .NET

You wouldn't realize that .NET is a cross platform solution by looking
at Microsoft's website. That's because to Microsoft, .NET is for the
Windows operating system. You have to look to a smaller company,
[Xamarin](http://xamarin.com/), and the 
[Mono community](http://www.mono-project.com/Main_Page) to find that they have
developed a fairly complete and production ready .NET implementation
over the past seven years. They've also created a fairly good IDE for
Mono called [MonoDevelop](http://monodevelop.com/). 

So why is .NET and
Mono the better solution? Well, you get the power of the .NET framework
of course. Mono currently supports up to .NET 4.0 with some features of
5.0 already working in the trunk. The .NET compilers are also quite fast
during compilation out of the box giving you major speed boosts over
C++. You also get WinForms support out of the box. That will give you
native rendering in Windows with mimicked results on the other operating
systems. Of course, this is only a starting point. Mono supports a
multitude of other UI frameworks including
[Gtk](http://www.mono-project.com/GtkSharp) and
[Cocoa](http://www.mono-project.com/MonoMac), giving you true native
drawing in all platforms. There's even
[MonoTouch](http://ios.xamarin.com/), 
[Mono for Android](http://android.xamarin.com/), and 
[Windows Phone 7](http://create.msdn.com/en-US/) frameworks to cover the mobile side.

The one issue you have when you jump to multiple frameworks, though, is
that you require multiple UI projects for the same solution. This will
be the downside of any project that will try to be native on multiple
platforms, no matter what the language. You can start developing using
WinForms and have a workable solution for all platforms. Later when you
want to add true native support, you can add in WPF, MonoMac, and
GtkSharp. At that point, it's up to you which frameworks to support with
no limitations.
