---
author: markglenn
layout: post
slug: grokking-sockets-physical-layer
status: publish
title: 'Grokking Sockets: Physical Layer'
categories:
- Grokking Sockets
tags:
- networking
---

After a short time of thinking, I've decided to focus on the 7 layers of
the [OSI model](http://en.wikipedia.org/wiki/OSI_model). We will be
building off the knowledge of each layer to see how they all work
together harmoniously and how we can trick them into going just a little
bit faster. I guess that makes this series an eight part series, so it's
going to be one long journey. Of course, this series isn't called "Kinda
knowing sockets," or even "Mastering sockets." It's called
[Grokking](http://en.wikipedia.org/wiki/Grok) sockets. That requires a
deep, xen like understanding of networking. And that includes layer one
of the OSI model, with all of its hardware goodness.

<!--more-->

Yes, if you look
again at the URL for this site, it will still say *code*fixes.com. Of
course, you can't master the art of software without knowing how what
your write turns into physical changes. In this case, how does the
information from one computer electronically get sent over to another.
This is not black magic (as much as the electrical engineers want us to
believe).

Let's first talk about the physical layer you may be most
familiar with, ethernet. You may see it as 10BASE-T, 100BASE-TX, or
1000BASE-T. These are the standards for communicating over copper wire,
which is what hides inside the ethernet cable. The wires are paired and
twisted together inside the
[shielding](http://en.wikipedia.org/wiki/Shielded_cable). They are
twisted and shielded to avoid [electromagnetic interference](http://en.wikipedia.org/wiki/Electromagnetic_interference).
The trick here is the twisted pairs carry opposite signals, known as
[differential signaling](http://en.wikipedia.org/wiki/Differential_signaling). This
means that if one wire gets interference, the other will too because the
twisted wires coupled together.

The other standard you probably know and
use is 802.11, or really IEEE 802.11. This is the standard for consumer
grade wireless networks and is pretty standardized in the corporate
world. It transmits wireless signals from one wireless adapter to
another using strange modulation acronyms such as
[DSSS](http://en.wikipedia.org/wiki/Direct-sequence_spread_spectrum),
[FHSS](http://en.wikipedia.org/wiki/Frequency-hopping_spread_spectrum),
and
[OFDM](http://en.wikipedia.org/wiki/Orthogonal_frequency-division_multiplexing).
Basically, all of these describe how to use the wireless frequencies
assigned to each standard. The basic idea is that wireless has to deal
with more interference than a physical wire. Think of your radio in your
last car (because maybe you have one of those fancy HD radios now). When
you were far from a radio station, sometimes you heard two stations
switching back and forth within the static. This is what radio
frequency, or RF, interference "sounds" like.

These radio stations are
given dedicated bands of space by the FCC (in the U.S.). That means they
are guaranteed that band by the government. WiFi does not have that
luxury. Everyone needs to play nice and share the same bands. Worse yet,
the transmission performance is so poor on these bands, that the FCC
didn't want it and has opened it up to anything. That's why we see
2.4GHz cell phones, 2.4GHz wireless keyboards/mice, and 2.4GHz
bluetooth. Everything is on this band and we want to get over 100Mbps to
our PCs.

That's where the complicated spread spectrum type modulations
come into play. At its most basic level, a signal is transmitted on a
coded set of frequencies that is agreed upon by the sender and receiver.
This is called [code division multiple
access](http://en.wikipedia.org/wiki/Code_division_multiple_access).
Since the frequencies are coded, another sender can send on a different
code simultaneously. The receiver then takes the full spectrum, and
using advanced math that is above my level, extracts or de-spreads the
original transmission.

There are further ways of handling interference
such as 802.11n's use of [orthogonal frequency-division
multiplexing](http://en.wikipedia.org/wiki/Orthogonal_frequency-division_multiplexing).
It uses multiple signals,
[subcarries](http://en.wikipedia.org/wiki/Subcarrier), and higher level
math than the previous versions. If you're really interested, or just a
glutton for punishment, you can read more about it on Wikipedia.

So what
does this all mean for us coders? Well for one, you can now impress your
engineer friends by using acronyms such as CDMA and complex vocabulary
such as "orthogonal subcarries". But in reality, we need to know one
thing out of all of this. Interference is our main source of slowdowns
in layer 1 of the OSI model. So, we have a few options to think about.
If you need the dedicated bandwidth, go with a wired connection. This
will give you some level of guaranteed bandwidth, although there are
some things to worry about higher up the OSI model.

If you have to use
wireless, know that you may lose large chunks of your data. If you're
using TCP, this equates to large lags and drops. You can avoid some
interference by switching channels on your routers and making sure two
routers near each other are on orthogonal frequencies. This will avoid
interference between the routers and minimize the crosstalk between
computers on different routers.

You can also switch bands all together
to the 5GHz band. There will be generally less interference on this band
right now since most consumer grade electronics don't use it. Plus the
added benefit of 802.11n's four simultaneous open channels using
[multiple input, multiple
output](http://en.wikipedia.org/wiki/Multiple-input_multiple-output) and
its multiple antenna array for allowing directional transmission will
give you much higher performance with much less broadcast noise.

Also,
since 802.11n is an open ended standard in some regards, you will find
that the expensive hardware will actually out perform the cheap stuff.
So, if you need the bandwidth, get ready to pony out a lot more money
for a router that has higher coding rates and more simultaneous streams.
These babies can get up to 600 Mbps (theoretical), if you have the right
hardware.

So now that you know the basics of the first layer of the OSI
Model, we can continue building upon that knowledge to understand the
next article in this series about layer 2, the data link layer.
