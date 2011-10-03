---
author: markglenn
layout: post
slug: ui-programming-youre-doing-it-wrong
status: publish
title: 'UI Programming: You''re Doing It Wrong'
comments: true
categories:
- .NET
- Multithreading
- Programming
tags:
- c#
- threading
- ui
---

{% img right /images/blog/hourglass.jpg "hourglass" %}
Let me ask you a question; a serious question. How are you handling events
in your GUI applications? Are you just running code whenever an event
comes? Is your application trying to work well with others? 

Now tell me, does it match the following?

``` csharp
public void OnClick( EventHandlerArgs args )
{
    ThreadPool.QueueUserWorkItem( _ => DoTheWork( ) ); 
}
```
If it doesn't, you may be irritating your users.

<!--more-->

So what can we do? Well
your processing power is a limited resource, especially when we talk
about the user interface. You need to treat it like the rare commodity
that it is. If the cost of processing power on the user interface thread
actually did cost you money, you would do anything you could to avoid
using it. Well that's how your user feels. Every millisecond on the the
UI thread is another millisecond your user has to wait. It might not
seem like much, but an unresponsive UI is a problem. It's hard to see
and even harder to test. You just know if something is unresponsive.

To fix this we need to move everything off the UI thread... I mean
everything. Well, as you know, not everything can be on the background
threads. You need still need to handle events and physically update the
screen. These things are inherent to operating systems and GUI
frameworks. Even *if* you could, the display updates all at once. So we
work around these things by doing the bare minimum. The instant we are
on the UI thread, we queue up work on the thread pool.

I told you before
that multi-threading is difficult. Well, that is true, but it's an issue
you will have to deal with eventually. I will go into more detail in the
future, but for now, just lock everything that you need. Don't worry
about efficiency on the background threads. It's already in the
background, so it shouldn't bother the user to wait an extra hundred
milliseconds. If you find that something is taking too long because it's
waiting on a lock, then you can go and optimize it using functional
style programming or non blocking operations.

Now the GUI is responsive.
Button presses are handled instantaneously and switching tabs happen
right when the user clicks. Everything is great, except for the fact
that there is no response to a user clicking the button. All it does is
press in and out. No user feedback besides that. What happens if the
background process requires multiple seconds to run? Well, you need to
notify the UI thread.

This is where the BackgroundWorker comes into
play. The ThreadPool.QueueUserWorkItem is fine for those quick processes
you need to fire off, but we need something for the long running tasks.
BackgroundWorker can access the UI thread whenever it's needed. That
means you can update the status of the process and notify of completion
whenever you need and not worry about whether or not you're on the
correct thread.

Let's look at how we use it.

``` csharp
// Create the worker 
var worker = new BackgroundWorker {
    WorkerReportsProgress = true,
};
```

We're reporting progress in our example, so we need to tell .NET about that.
``` csharp
// Does the actual work 
worker.DoWork += ( s, a ) => { 
    var w = ( BackgroundWorker )s;
    for ( int i = 0; i < 10; ++i )
    { 
        // Slow process... zzzz
        Thread.Sleep( 1000 );

        // Report the progress
        w.ReportProgress( i * 10 );
    }
    
    // We're done 
    a.Result = "Success";
};
```

Here we're running a slow process to show that the user interface is still usable.
If you did this on the UI thread, the application would lock up for a
full ten seconds and would never update the display. In this example,
it's harmlessly locking up a background thread.

``` csharp
// Will run on the UI thread
worker.ProgressChanged += ( s, a ) => { 
    // Progress has changed
    progressBar.Value = a.ProgressPercentage;
};

// Also run on the UI thread 
worker.RunWorkerCompleted +=
    ( s, a ) => MessageBox.Show( ( string )a.Result );

```

Now we can update the user interface. The progress bar will update every second, and we didn't
have to check which thread we're on.

``` csharp
// Run the worker on the threadpool 
worker.RunWorkerAsync( );
```

That's all that's required to run something in the background. Why would you even
think of trying to do it in the foreground?
