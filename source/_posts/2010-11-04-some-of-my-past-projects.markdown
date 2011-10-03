---
author: markglenn
layout: post
slug: some-of-my-past-projects
status: publish
title: Some of my past projects
comments: true
categories:
- General
tags:
- c#
- c++
- programming
---
Over the years, I've of course worked on a ton of projects, and some of them I
open source. Usually I do this if the project was school related, back when I
was in college, or I want to hand over the project to the community. Of course,
neither go very far after that since it seems like you need to be known and you
actually have to build something useful.  Anyway, here I'm going to list some
of those projects and where you can find them. 

<!--more-->

Back when I was young, I made a program that converted a text file into an exe.
This allowed shareware vendors to create self running catalogs. It was a pretty
neat program, and had search, colors, mouse support, etc. I called it CatGen,
and I even sold a copy or two.  Not technically open source, but it built you a
.BAS file (QBasic/QuickBasic) that included the text file. You can find it here
(warning, not coming from a controlled source): 
[CatGen 3.0](http://piotrkosoft.net/pub/mirrors/simtelnet/msdos/basic/catgen30.zip).

I went on and started looking into 3D graphics, and at one point I wanted to
become a game programmer. I studied all the latest books on OpenGL, DirectX,
SDL, etc. It was fun, and I created my own game engine from it. I submitted it
as my senior design project in undergrad. It was a full blown Quake 2 engine
including rendering, physics, animations, sound, and music. I have to go find
that code.

{% img /images/blog/screenshot1.jpg "Quake 2 style engine" %}

I went on to work for Motorola after college. I was working in a research and
design group in the cell phone division. I was actually working with the people
who designed the original RAZR, and my pride and joy was the "morphing" phone
called the MOTOROKR E8.

{% img /images/blog/motorola-rokr-e8-combo.jpg "Motorola ROKR E8" %}

I wrote all the software for the original prototype, and helped in analyzing
and fine tuning the morphing, capacitive sensor, and the
[haptics](http://en.wikipedia.org/wiki/Haptic_technology). By the way, the
haptics on this phone were amazing. Pushing down on the buttons felt exactly
like a button, even though the keyboard didn't move.

I decided to move on from there when the company was doing poorly, but I did
take something with me. I took the idea I was using for the user interface and
made it my own open source project (with the okay from my boss at the time). I
called it [MiniUI](https://sourceforge.net/projects/miniui/). This was a
hardware accelerated, [scriptable](http://www.lua.org/) user interface. It
allowed all the effects we take for granted on our smartphones now to be
created simply and easily through XML and simple scripts. I wrote two papers on
the project which can be found through the following:

-   [http://sourceforge.net/projects/miniui/files/Documentation/1.0/MiniUI.pdf/download](http://sourceforge.net/projects/miniui/files/Documentation/1.0/MiniUI.pdf/download)
-   [http://sourceforge.net/projects/miniui/files/Documentation/1.0/ctirs08\_submission\_4.pdf/download](http://sourceforge.net/projects/miniui/files/Documentation/1.0/ctirs08_submission_4.pdf/download)

I also have a [demonstration video](http://video.google.com/videoplay?docid=-4422339729517928865#), but it
is pretty low quality and the recording was very laggy (hence the tearing on
the screen).

To this day, that project still gets downloads, but I'm not sure why. It's now
2-3 years dated. It also started getting more hits since I started this blog,
but that is probably just be coincidence. Otherwise, I'd start believing you
guys are stalking me.  

Lastly, we come to my latest project. At my company, I created a data access
layer for an application framework we use from
[Aptify](http://www.aptify.com/Home.aspx). It's an adapter of NHibernate and
NHibernate.Linq to their proprietary system. It's actually fairly complex, and
after doing it I wonder why I finished it. Now that it's done, though, we're
loving it. I submitted it to Aptify for their Aptify Innovations Award contest.
I was one of the top finalists and spoke at their user conference in Las Vegas.
After presenting my work to their community, the community voted me as the
winner. 

So I guess that makes me an award winning developer, although it's a fairly
niche area. You can find my project up on bitbucket at:
[http://bitbucket.org/markglenn/apics.core/src](http://bitbucket.org/markglenn/apics.core/src).

So what now? Well I'm currently working on a commercial client product in the
message queuing market. Hopefully I can get that to the market in the next
couple of months. In the future I'll discuss more about the product as I build
it. For one, I have a lot of interesting things to talk about in regards to
some of the tools and middleware I'm using to create it.

Also, again, I'm going to [Startup Weekend](http://startupweekend.org/) next
weekend in [Chicago](http://chicago.startupweekend.org/). Actually if you go to
that link, the [top story](http://chicago.startupweekend.org/coders'-survival-guide-to-startup-weekend/)
(as of this writing) may [look familiar](http://www.codefixes.com/2010/11/coders-survival-guide-to-startup-weekend/).
Yes, it's my article!  Chris, one of the people running Chicago Startup
Weekend, asked to republish my article on the site. So I'm a proud guest writer. Not bad for a guy who got B's and C's
in english and writing classes. Anyway, I hope to see you there.  Also make
sure you have your [tickets for the event](http://www.eventbrite.com/event/936652553).
