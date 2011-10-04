---
author: markglenn
layout: post
title: "Grokking Sockets: Data Link Layer"
description: "Grokking Sockets: Data Link Layer"
keywords: grokking,sockets,data link layer,programming
comments: true
categories:
- Grokking Sockets
tags:
- networking
- programming
---

I know I've scared away a lot of my audience when I started talking
hardware last time. Well, do not fret because we are starting up the
stack with a software (firmware) layer. The data link layer is how we,
the software guys, fix the problems incurred on the hardware. It's the
layer that does the communication from one computer to another; what
actual bits are being sent. It also detects bit errors if for whatever
reasons the data is corrupted. It's an important layer, although easily
forgotten because it's usually handled by your network card. Even though
it's hidden, you need to understand it because it is the final step in
transmission before hardware. 

<!--more-->

The [data link layer](http://en.wikipedia.org/wiki/Data_Link_Layer) is the first step
in managing the connection between two network adapters on the same LAN.
It really has two main jobs, and in 
[IEEE 802](http://en.wikipedia.org/wiki/IEEE_802) networks is defined as two
separate sublayers. The first, or lowest of the two, is the 
[Media Access Control](http://en.wikipedia.org/wiki/Media_Access_Control) (MAC)
sublayer. You may recognize the acronym MAC from the MAC addresses
printed on your network cards. This is the first address used in socket
communications. The MAC address is a globally unique address flashed
onto the network adapter's ROM space. This address is what is added to
each frame that is sent out, and it's what is monitored to see if a
frame needs to be read. 

Of course, that's not the only thing it has to
worry about. If we have a group of computers on the same LAN, we would
have interference. Imagine that instead of computers, we have a group of
people sitting at a small table. One person can't just start talking
without listening for silence first. If every person started talking
without listening for silence first, all we would hear is noise. While
some protocols can pick out streams from noise, like picking up a
conversation by the sound of one person's voice, but most of the time
you're stuck with one speaker at a time.

Some of you may have noticed a
problem. If two people are listening and hear silence, they may on
occasion start talking at the same time. In the case of two people, they
will usually hear this and go back and forth saying "No, you go first."
In the case of the MAC sublayer, a simpler process of random delays
after a collision occurs. Each network adapter chooses a random wait
delay and then tries again. In the case of another collision, a new
larger random number is chosen. This is called 
[carrier sense multiple access with collision detection or CSMA/CD](http://en.wikipedia.org/wiki/Carrier_sense_multiple_access_with_collision_detection).

The MAC sublayer also handles frame synchronization. It determines at
which bit a frame starts and ends. This is done through different
methods and varies based on standards. The usual method is to stuff a
special sequence of bits or bytes at the beginning and end of a frame.
These are known as 
[start of text (STX) and end of text (ETX)](http://en.wikipedia.org/wiki/C0_and_C1_control_codes) sequences.
So if a receiver notices an ETX sequence at an unusual point, it knows
that the frame has been corrupted.

The other sublayer is the 
[Logical Link Control](http://en.wikipedia.org/wiki/Logical_Link_Control) (LLC)
sublayer. While the MAC sublayer can detect frame errors of size changes
or missing bits, it alone cannot detect bit errors. For example, if say
the frame is 1500 bytes long, and only one bit has been incorrectly
inverted, the MAC sublayer would never know. In this case, the LLC
sublayer adds the
[CRC](http://en.wikipedia.org/wiki/Cyclic_redundancy_check) value of the
frame to the end. This will detect nearly all the bit errors. 

The LLC also handles flow control. When a sender sends out a frame, it expects
the receiver to acknowledge its arrival. In simple cases, the sender
would wait for the acknowledge packet before sending the next. This way,
the receiver determines the rate at which packets are sent; how fast the
receiver can receive. Of course, there's a delay using this method known
as a [round trip delay time](http://en.wikipedia.org/wiki/Round-trip_delay_time) (RTT). To get
around this, most processes support a 
[sliding window protocol](http://en.wikipedia.org/wiki/Sliding_window_protocol). In
simple terms, a sliding window allows for a range of packets to be on
the line waiting for ACK packets. Ideally the window size would allow
enough packets to be sent to cover the RTT. This would ideally make the
transmission continuous. 

Next time we'll be discussing the next layer up, the network layer. This is where the fun job of routing occurs and
where software decisions can start to be made.
