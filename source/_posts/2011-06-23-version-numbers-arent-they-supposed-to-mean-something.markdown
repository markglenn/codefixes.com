---
author: markglenn
date: '2011-06-23 21:22:03'
layout: post
slug: version-numbers-arent-they-supposed-to-mean-something
status: publish
title: Version numbers... Aren't they supposed to mean something?
comments: true
categories:
- General
---

<img src='http://www.codefixes.com/wp-content/uploads/2011/06/google-chrome-version-300x171.png' alt="google chrome version" style='float: right' />

Software that's been out for many years: v0.71. Google Chrome that's
been out for a short time: v12.0. What has happened to version numbers
that meant something? They have become a way of trying to show market
dominance, or a way from hiding from your users. Worse is the software
that is so afraid of version 1.0 that they will increment so slowly that
we don't know if it's worth upgrading. Looking at a version number for a
piece of software no longer tells me anything.

<!--more-->

Many of you will argue that version numbers never had any true meaning.
This may be true for many commercial applications. A large version
number shows that you've been around for a while, and it's a great way
of deceiving without anyone really noticing. Minor version numbers were
just incrementers no matter how large or small of a change.

I was bitten by this recently at my job. We are still stuck on ruby
1.8.6, however we are looking to upgrade to 1.8.7. One of the great
benefits of ruby and rails is gems and bundler. A gemfile stores the
names and versions of all the required ruby gems in your project. Even
better, you can specify a versioning system for each gem to
automatically update when asked. This is great, if the gems stay with
versioning standards.

However, one gem did not follow any standards and released a maintenance
release that no longer supported ruby 1.8.6. Since we only locked down
our gem to the second decimal point, this came down the pipeline to our
development machines causing all sorts of new errors in our tests.

The response from the developer was "I told you 1.8.6 was deprecated."
Yes, but we expect deprecation warnings to affect us on the next fairly
major release. This was a breaking change, however the version number
did not denote this. I wish I had the time to read the release notes of
every gem, but this is just not possible. I made an assumption based on
the version number and was bitten by it. You may say that this is my
fault for allowing the update, and you would be right. It's something
that I will not repeat in the foreseeable future. However, based on my
own Googling of the error message, I obviously wasn't the only person
that ran into this problem.

## Keeping up with the Joneses

Remember Java 1.2? I do, and it wasn't all that long ago. How about 1.3,
1.4? Do you remember Java 3 or 4, though? No you don't. That's because
they never existed. Java 1.5 was labelled "Java 5" and Sun (now Oracle)
never looked back. This was back when .NET was version 2.0 already
making Java seem like old news. The name, "Java 5" sure looks more
appealing against .NET 2.0/3.5/4.0. Sun also did this with Solaris
jumping from v2.x to v8. Marketing material magically removed any
reference to their old versioning scheme.

This is not limited to Sun, however. Winamp jumped from v3 to v5
because, as their marketing states, it was a combination of v2 and v3.
Since v2 + v3 = v5, this is what they decided on. AOL seemed to release
a new major version every few weeks. Netscape skipped versions 5 and 6
to catch up to Internet Explorer. Many times these major version
releases hardly warranted these numbering changes. This is what happens
when marketing is allowed to take over version numbers.

## It will never be truly finished

This is the exact opposite problem that plagues many open source
projects. Open source projects are afraid of the v1.0 stigma; that the
program needs to be stable. Instead they will release v0.19.37a (okay, a
little facetious). This makes it more difficult to believe that this
software is ready for production, but nonetheless, it is.

As a reborn programmer into the Ruby on Rails realm, I have been shocked
at the number of gems used in production that are no where near v1.0.
It's not that they aren't production ready. On the contrary, many of
these gems are rock solid. It just feel a bit weary when it looks like
the authors don't believe it's v1.0 worthy.

One response to this is that the developers feel that it's never truly
finished. MAME is one to use this excuse going as far as going from
v0.99 to v0.100. What these projects fail to realize is that there is
life after v1.0. There's actually v2.0, v3.0, and so on. Heck there is
an infinite amount of version numbers just waiting to be taken. If
anyone needs some, I have some extra version numbers lying around that
I'm willing to give out for free.

## What I believe in

I'm sure it's difficult to listen to someone standing on his soap box
decreeing what people should or should not do with their version number,
especially when there does not seem to a hard and fast rule for version
numbers. Instead, what you should do is read more on version numbers and
what prior, successful projects have done. I just give one way of doing
this that makes sense to me.

I believe in the [major].[minor].[maintenance] versioning system.

Major is for major changes in the software. This can even include enough
changes to warrant a paid upgrade. When I see a major version change, I
expect and understand breaking changes. I also expect new features, not
just bug fixes.

Minor is for minor updates. These may be small feature additions, major
bug fixes, etc. This can include some breaking changes, but fairly
minor. I should be able to look at the release and fix whatever breaks
within a few hours.

Maintenance is for just that, maintenance builds. This should absolutely
not include any breaking changes. It also should not have any new
features. This is just bug fixes. Leave it at that.

Another example of a good versioning scheme is Ubuntu's month.year.point
versioning. I know right off the bat that 11.04 is the latest major
version and that significant changes have occurred since 10.10. Although
this does contradict my version inflation talk above, it is a well known
versioning method for Ubuntu users and very consisten. It's not just
marketing telling developers that we need to skip a few versions to
catch up to our competitors.

Following a standard will always make things easier for your users. It
doesn't have to be the major, minor, maintenance style that I show
above, but stick to a versioning scheme that fits for your project and
users.
