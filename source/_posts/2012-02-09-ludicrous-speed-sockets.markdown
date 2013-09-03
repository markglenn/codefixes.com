---
layout: post
title: "Ludicrous Speed: Sockets"
date: 2012-02-09 08:15
comments: true
categories: sockets
---

With the popularity boom of internet and intranet based software solutions, and the push for more
[Service Oriented Architecture (SOA) systems][soa], network software usage is at an all time high.  Of
course, many of the systems created are built upon highly abstracted frameworks, so they don't 
have to worry much about sockets.  However, there is a high demand for working on those 
frameworks and internal networking software that requires a deep knowledge of network systems and 
pushing the speed limits on the same hardware.  

In a previous life, I worked on high speed trading software where our traders worried about
millisecond delays.  We pushed and received so much data that a standard [TCP][tcp]/[UDP][udp] system could not
come close to keeping up, even on multicore machines with gigabit connections.  What this describes
is a post-mortem of my learning process.

<!-- more -->

One of the downsides of the huge popularity in networking is that at a certain point, the hardware
and firmware guys took away our control.  Most of the network stack is done directly on the network
hardware with the help of the device drivers running in kernel space of the operating system.  This gives
the benefit of "hardware acceleration" at the cost of customizability.  While code can be written to operate
at lower layers than the [transport layer][transport layer], most of the time these will run slower due 
to multiple layers of abstraction from the hardware.  We will focus instead on working with what is given.

There are large and expensive packages that try to solve these problems from companies such as 
[Tibco](http://www.tibco.com/) and [29West](http://www.informatica.com/us/products/messaging/). 
From my time working with them, they are worth every penny if you can afford it and you work in
a problem space that requires that level of throughput.  However, for us peons, we have some options that
can help improve our throughput speeds.

Now, I spend all my time giving examples and micro benchmarks of all possible optimizations I'm offering,
but what I've found is that networking is a little bit like black magic.  There are so many variables
involved that determine final output speed that my benchmarks will not match anything you create, even
if we use the same exact algorithms.  Things such as network latency, number of hops, solar flares, the number
of flaps of a butterfly's wings while traveling from tree to tree outside your window; all cause random differences.
Don't focus too much on the numbers involved with network programming, but instead focus on the concepts.

UDP for speed
-------------

The first thing you learn when trying to do high speed networking is that you should pull out UDP.  This
is an obvious choice due to the fact that there is no overhead of [acknowledge (ACK) packets][ack] that come with
other reliable transport services.  You will find that most real-time games use UDP because it can push
out the raw speed with minimal delay.  

This is because UDP packets are about as raw as you can get on standard home and commercial hardware.  There 
is no flow control, no delivery confirmations, and no guarantee that the packets even arrive in the same order.

UDP is good for fast, streaming data.  When you care more for fast packet delivery than you do for guaranteeing
that older packets arrive.  You'll commonly find it being used for streaming video since that data has 
hard real-time requirements for delivery.  Video codecs normally have error correction built into the 
algorithms because they know they *will* lose packets.

In the trading world, stale price quotes were normally worthless when newer quotes were available.  We streamed
price quotes as UDP datagrams because we only cared about up to date pricing.  We did lose packets, especially 
on huge bursts of data, but that was okay in moderation.

TCP for reliability
-------------------

Not all data is so easily ignored, however.  Most data requires guaranteed delivery.  Just think, if you 
were browsing your favorite site and small chunks of data were missing from the page and every once in a while
an image was mangled.

TCP gives the client server an agreement on the data.  The data *will* arrive on the receiver's side,
the data **will** arrive in order, and the data *will* be correct.  This is great for files, especially 
larger ones that require multiple packets to send it in whole.  The receiving software won't need to 
worry about those issues and can use the connection to stream data in correct order.  If you need 
reliability, you won't find any protocol that beats TCP on protocol availability and data validity.

The price of those guarantees is great, though.  If you need any type of throughput, you will find
yourself lagging.  When I was building a prototype phone for Motorola, we were using a PC to take readings
from multiple sensors on a phone over an 802.11 wireless connection for real-time and post processing.
The data wasn't all that large or fast, but we constantly got lagged responses because TCP would hold us up.
Because we didn't have time to rebuild it for UDP reliably before a demo, I would SSH into the phone
while someone demonstrated it and would reset the socket connection every few minutes while he was holding
it to get it back working reliably.  "Ignore the man behind the curtain."

TCP includes a buffer called the "[sliding window protocol][sliding window]" buffer.  It will hold a certain number of packets in order
on the receiving side so it can send them off to the client software properly.  This buffer is quite small
and can be easily overflowed, especially on an unreliable network connection such as wireless.  When that
happens, the protocol will start throwing away perfectly good packets it receives until it can catch
back up.  This was what was happening on our phone prototype.  While our network monitor showed great
throughput, most of the packets were being thrown away because of one single missing or bad packet.  We also
lost throughput since the flow controller would start backing off on the speed until the PC could keep up.

Join the two sides
------------------

We have these two two popular protocols that seem to be mutually exclusive.  Nothing can be further from
the truth.  Instead, you should join forces and use both protocols, just on separate connections.  Have
your stream of unreliable data on one UDP connection and the rest of your data on TCP connections.

Operating systems and network hardware have built in mechanism, called "[Quality of Service][qos],"
to actually slow down a single connection so one hoggy connection cannot take over an entire network 
(although how well this works hugely depends on the quality of their QoS algorithm).  Yes, this is an
over exaggeration of the truth, but it presents the idea simply.  To increase throughput despite QoS
systems, you should increase the number of connections.  On a side note, including multiple TCP 
connections also increases the size of your sliding window buffer by a multiple of the number of 
connections.

Threaded service
----------------

This is probably the most important piece, that I question putting it way at the bottom of this article.
When you write a socket program, what do you do with a packet the instance you receive it?  If you said
anything besides buffering it into a queue, you are doing it completely wrong.

The sockets library has an odd system for how you access the receive buffer.  Instead of receiving a
notice that a packet is available to grab, we are notified that the receive (Rx) buffer is ready to be
read, and only if we specifically ask to be notified for the next available stream of bytes.  What this
means is the data will stay within the network buffer until you go and read it.  And while you are reading
from the socket, you could be (and will be, at a certain throughput) losing data.

To minimize this data loss, you need to take the data off the network stream, put it directly on your
internal packet queue, and enqueue another asynchronous (or threaded synchronous) read.  Don't try to parse
the data.  Don't try to analyze what packet you just received.  Don't even create a byte array to host the new
packet.  Just pull the packet and put it in your queue.  Many asynchronous socket libraries (such as [ASIO][asio])
require a buffer to place the data within, so make sure you have those packet buffers already created.  Use
a memory pool of byte arrays if needed.  Reuse these buffers as much as you can.

The quicker you get to the next read statement, the less likely you will lose packets.  Although I would 
love to see multiple queued up reads available from the socket library (you can do this over USB, for
example.  I once queued up 10,000 reads simultaneously over USB to max our throughput.), it doesn't yet 
seem available.

Even if you use a non-blocking library such as [I/O Completion Ports (IOCPs)][iocp], you need to follow these same rules
because the same results will occur.  At the trading firm, we would normally lose packets when using 
IOCPs because we had the same thread reading from the socket along with parsing them out.  Non blocking APIs
still have to follow the same rules we do, so don't expect that using one will allow you to ignore these issues.

Oh, and by all means, never use the UI thread to do any networking.  You'll find that just drawing to the display
can cause networking problems due to the delays.

TLDR: Too long. Didn't Read
---------------------------

* Use UDP when you can get away with lost packets, but need the speed.
* Use TCP when you need guaranteed data.
* Use a combination of the two on multiple connections when you need both.
* Use more than one connection to maximize throughput.
* Don't do anything other than read from the socket on the receiver thread.

[soa]: http://en.wikipedia.org/wiki/Service-oriented_architecture
[iocp]: http://en.wikipedia.org/wiki/Input/output_completion_port
[qos]: http://en.wikipedia.org/wiki/Quality_of_service
[ack]: http://en.wikipedia.org/wiki/Acknowledgement_(data_networks)
[transport layer]: http://en.wikipedia.org/wiki/Transport_layer
[tcp]: http://en.wikipedia.org/wiki/Transmission_Control_Protocol
[udp]: http://en.wikipedia.org/wiki/User_Datagram_Protocol
[sliding window]: http://en.wikipedia.org/wiki/Sliding_window_protocol
[asio]: http://www.boost.org/doc/libs/1_48_0/doc/html/boost_asio.html
