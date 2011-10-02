---
author: markglenn
date: '2010-11-23 23:19:56'
layout: post
slug: grokking-sockets-overview
status: publish
title: 'Grokking Sockets: Overview'
comments: true
categories:
- Grokking Sockets
- Programming
tags:
- networking
- programming
---

I've worked with socket programming on and off (mostly on) for a good
ten years. Although this doesn't make me an expert, by far, this has
given me good insight into what seems to work and what doesn't. This
will most likely be a multi-part piece as sockets are a complicated
beast. What I will be talking about is a very low level understanding of
how sockets work and what each of the seven layers of the OSI model mean
to you. Hopefully you will have such a level of understanding of sockets
and protocols that you will [grok](http://en.wikipedia.org/wiki/Grok)
them. Only when you reach this level can you understand how to max out
performance.

<!--more-->

As with many of my other posts, we're really here to talk
about maximizing performance. The world has changed with the advancement
of multicore processors and cloud computing. As we move into
distributing our work among multiple processors and machines, these
separate processes will need to communicate. The IP protocol is now
ubiquitous due to the internet's popularity. It continues growing as
processes are moved to the cloud and APIs are moved to RESTful sites.

So the [Open Systems Interconnection model](http://en.wikipedia.org/wiki/OSI_model) or OSI model defines the
basis of most networking systems. This includes the full stack that runs
the internet from HTTP down to the 802.3 standard (ethernet cable). I'll
briefly define each of the seven layers and how they map to the web.
Each layer of the stack adds its own unique wrapper upon the packet it
receives from above. In other words, the layers don't care about each
other. They just know they need to add some data to the packet as it
goes down the layers, and reads from the packet as it goes back up on
the other side.

**Layer 1 - Physical Layer** 

This is the one that's
probably the easiest to understand. This is the standard of actually
sending bits down the wire. This includes your standard ethernet and
wireless standards. This defines not only the signals and voltages, but
also the physical connectors and wires. There's not much for efficiency
that we can do on this layer since it's physical hardware and doesn't
allow for software modifications.

**Layer 2 - Data Link Layer**

The data link layer defines the protocol of talking between two machines that are
physically connected. 802.3 extends into this layer describing what each
byte means. This is also where your MAC address comes into play... you
know, that long hex string written on your network card. Again, this is
usually physical hardware, so not much we can do. If you have an
"ethernet" card, it will probably only speak ethernet. Flow control and
error checking are done here too.

**Layer 3 - Network layer**

Okay, this is where code starts getting thrown in, although mostly in firmware. You
may know this layer as the IP layer in protocols such as TCP/IP and
UDP/IP. The network layer defines how packets are routed from computer
to computer. This is mainly how far up routers and hubs go when it comes
to analyzing packets. They read up to layer 3, then decide the optimal
path this packet should travel. 

**Layer 4 - Transport Layer** 

This is
the basis of how one computer "sees" the other, even though they are not
directly connected. This is where TCP and UDP live. Decisions on how you
use this layer can affect your throughput and data quality. This is
probably the most important layer to grok to improve your throughput.
TCP is your connection oriented protocol, where the two PCs communicate
as if they were next to each other. UDP is the same, except the
connection state is not shared and the data may come randomly. 

**Layer 5 - Session Layer**

Layer 5 isn't all that important in the TCP/IP world.
It defines things such as VPNs and broadcasting methods. This is only
useful if you are building something custom. Otherwise, you would
normally just use an off the shelf component for this. Ignore it for
now.

**Layer 6 - Presentation Layer**

This is where things become a
little grey. The presentation layer defines how the packets work
together as a whole. That means if you're sending a file over TCP/IP,
while it may break up into packets, this layer will use them all as a
whole. This is straight code. It is normally the code that handles the
raw packets and converts them to useful information in your software.
Security is also added at this layer, so things like SSL live here.

**Layer 7 - Application Layer**

This is the bread and butter. This is
what the user actually uses and sees on the screen. After the packets
are pieced together in layer 6, your application must use that
information. This part of the application is usually run on the UI
thread, and normally does not interact with sockets directly.

In future posts, I will go into more detail about each one of the configurable
layers and describe steps that you can do to increase throughput.
