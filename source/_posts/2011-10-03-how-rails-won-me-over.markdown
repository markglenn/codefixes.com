---
layout: post
title: Why I chose Rails over MVC
comments: true
keywords: .NET,MVC,ruby,rails,programming
description: Ruby on Rails vs ASP.NET MVC and why I chose rails
categories:
- .NET
- Rails
- Programming
---

{% img right /images/blog/ruby_on_rails_logo.jpg 'Ruby on Rails' %}
As a C++ and .NET developer for most of my career, some people found it odd
that I would switch up and jump on the [Ruby on Rails](http://rubyonrails.org/)
bandwagon this late in the game.  I had fallen in love with
[ASP.NET MVC](http://www.asp.net/mvc) because the true simplicity of its web
development, and while I found some of the quirks of Ruby and Rails initially
annoying, I'm now a true believer in Rails and what it can do.

<!--more-->

You're probably thinking that this is just another post of how great rails is
and how you should come over to our side because we have cookies.  I'm trying
to write this as an objective view of Rails from a .NET developer's
perspective, so hopefully this won't come off as fanboyism speak.

{% img left /images/blog/asp_dotnet_mvc_logo.jpg 'ASP.NET MVC %}
I have been writing code in C# since v1.1 and the language itself has come into
being my personal favorite of the many I've used in the past.  It has near
native speed, fast compilation, and a fairly straight forward syntax.  But it
also includes a vast framework which now includes ASP.NET MVC.  Although
ASP.NET MVC isn't the first MVC framework, even for .NET, it's tooling support
in Visual Studio and simplicity has made it the fastest growing in the .NET
world.

Ruby on Rails on the other hand is fairly new to me.  I've been coding in it
for about a year between versions 2.1 and now 3.1.  While it's new to me, I've
found myself building web applications quicker and cleaner with it.

## Works in Notepad

I use notepad as an example here although I use vim.  What I'm really saying
here is the framework is easy enough that you don't need an IDE, IntelliSense,
or even documentation up if you are familiar with the framework.  This is not
so true with ASP.NET MVC due to the complexity of the .NET framework and the
amount of generated code.

## Quick Dev Time

My time is so precious, I didn't even have enough time to write "development"
in the header.  Okay, so that's not true at all, but I've noticed Rails to be
quicker in development even though I'm an average ruby programmer and pretty
fluent in C#.  This mostly comes down to the simplicity of the framework and
the minimal amount of physical typing that's required.

ASP.NET MVC has improved greatly to reduce the amount of code that's required
to build an application, but it still has a way to go.  Ruby may have the
advantage here because it's a dynamic language and simpler to add duck typing.
While .NET supports multiple dynamic languages, it still has to limit itself to
the lowest common denominator with static objects with some dynamic thrown in.

Also, while ASP.NET MVC 2 and 3 are pushing hard for the user to run with
ADO.NET Entity Framework, it still doesn't make a default choice for the
developer.  While this shows the framework is open to choice, it makes initial
development one step more difficult.

## Gems

If there was one thing that should make anyone look another time at Ruby on
Rails, it's the huge number of ruby gems available.  Microsoft has had a good
push lately with their NuGet packages and the market has seen a quick explosion
of popularity, but it's still hard to browse for packages unless you know them
before hand.  Mostly this is because there seems to be less discussions on
popular NuGet packages on the Internet.  I'm hoping that the tooling in Visual
Studio 11 fixes some of that and people talk more about their favorite NuGet
packages.

On the other hand, I know that in a new Rails application, I'm going to pull in
[Devise](https://github.com/plataformatec/devise) (authentication),
[CanCan](https://github.com/ryanb/cancan) (authorization),
[Haml](link:http://haml-lang.com/) (view renderer),
[RSpec](link:http://rspec.info/) (testing), and
[Will Paginate](link:https://github.com/mislav/will_paginate) (pagination).  With
these, I've gotten at least a weeks worth of work, if not more, compared to
having to build some of those by hand in ASP.NET MVC.  It's a nice feeling to
know you won't have to write yet another pagination partial.

## Tools

Okay, this one I know is going to be widely controversial.  Visual Studio is by
far the best IDE built.  Period.  End of story.  If you use even 10% of the
features it has, you will have to agree with me.  However, I now work almost
exclusively with Macs and Linux machines.  This means I cannot use visual
studio.

We have a pretty good alternative with MonoDevelop which I use quite often now,
but the tooling for MVC within it is mediocre at best and only really supports
V1 and some parts of V2 of the MVC framework.  

The Rails community follows more along the lines of the Linux and Unix
mentality of having tools do one thing and do them well.  With the fact that
everything runs separately, I can have a script run things automatically for
me.  This is exactly what I do with link:https://github.com/guard/guard[Guard]
which runs my unit tests automatically every time I save.  It also alerts me on
success or failure using [Growl](http://growl.info/) so I don't have to
interrupt what I'm doing.

## ASP.NET MVC Not a Bad Choice

If you're a .NET developer, this is not going to change your mind.  ASP.NET MVC
is still a solid choice, especially if you have existing .NET code you need to
interact with.  Microsoft, in a short period of time, has built up a great
framework that competes with Ruby on Rails and
[Django](https://www.djangoproject.com/).  This hopefully opens your mind a
little to the other options that may exist.
