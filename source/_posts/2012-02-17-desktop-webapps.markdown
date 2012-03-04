---
layout: post
title: "Desktop WebApps"
date: 2012-02-17 17:42
comments: true
categories: 
published: false
---
There's no denying the impact the world wide web has had on the world of software.  
We went from simple text and occasional image pages to full blown applications that use 
hardware accelerated graphics, asynchronous method calls, and genuine user 
interaction.  There is also no denying that a huge reason for this has been simple
to use web frameworks and the bare knuckle brawling competition between browser developers.

Browser developers have recently pushed forward with interoperability between their software, allowing
more complex functionality that can work across multiple platforms and browsers.  No longer
do you have to worry about this layout, or this event handler working in both Google Chrome and 
Mozilla Firefox.  Of course, during all that time, desktop application frameworks haven't been so lucky.

<!-- more -->

Cross platform desktop applications are notoriously complex to build.  The UI frameworks used for
each platform are completely non-compatible.  Even the old lowest common denominator of using C or 
C++ is no longer true with Cocoa for Mac OS X exclusively using Objective-C.  Some of the newer
UI functionality found in Windows 7 today is not even accessible unless you use a managed
language such as C# or VB.NET (or a hybrid approach with Managed C++).

To say HTML and CSS are the epitome of user interface definition languages would be a huge exaggeration 
of the truth.  Opinions aside, there is one thing the HTML and CSS have over Cocoa, WPF, and GTK+.  
They are truly cross platform.  Browser developers have scrutinized for years on this fact.

Of course, I would be amiss if I did not mention Java's Swing and Nokia's Qt frameworks.  These both offer
similar levels of cross platform capability as HTML, CSS, and JavaScript.  ...

Embed WebKit
------------

WebKit can be embedded as a component in most UI systems.  Think of it as just the UI layer that just
happens to be highly sandboxed.  It's the framework used to power Google Chrome and Apple Safari, two
very popular browsers.  We know that the capabilities of this framework can rival just about any other
UI framework in terms of speed and functionality, it just lacks a decent programming language.  It also 
requires the need for a client/server setup, something that many desktop applications don't need.

I'm working on a project currently that uses the Qt Framework with the Python library PySide.  However,
the idea I propose can easily be transposed into Qt and C++, Objective C and Cocoa, .NET and Internet Explorer,
or any other setup that gives you access to the inner workings of a web UI framework.  By accessing some of
the events that the browser engine sends out internally, we can handle most tasks without hitting the network.

....

Think in JSON and HTML
----------------------

For desktop applications, you usually have two methods of displaying something to the screen.  The first,
and possibly the current most common, is to push data by writing to a display widget.  For example, in C#
and WinForms, you would normally do something like the following:

``` csharp
// Somewhere on the UI thread
myLabel.Text = "Hello World!";
```

The other option is to do a pull like setup with binding from the user interface.  Again, with an 
example from C# and WPF, we would do something like this:

``` csharp MyViewModel.cs
// Assuming a basic MVVM framework
public class MyViewModel : ViewModelBase
{
    private string helloMessage;
    public string HelloMessage
    { 
        get { return this.helloMessage; }
        set
        {
            this.helloMessage = value;
            NotifyPropertyChange( "HelloMessage" );
        }
    }
}
```

``` html MyView.xaml
<TextBlock text="{Binding HelloMessage}" />
```

Web developers haven't had the luxury of being able to directly share date between the server and web
browser.  Instead, they needed to break away from these ideas that data can be so tightly coupled with 
only a single instance of a value in memory that's shared between the UI and code.  The idea was to 
pass data as straight html updates or as serialized data, such as XML or JSON.  The benefit they created
was a completely independent view that was completely disconnected from the host process.  HTML is a 
stateless protocol, so shared memory or even an open, but idle, connection was very difficult to impossible.

We would mimic this by passing serialized data to the browser as JSON strings.  
