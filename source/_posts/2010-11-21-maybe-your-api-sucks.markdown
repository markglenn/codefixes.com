---
author: markglenn
layout: post
slug: maybe-your-api-sucks
status: publish
title: Maybe Your API Sucks
categories:
- .NET
- Programming
- Ruby on Rails
tags:
- programming
---

This goes back to my love/hate relationship with Ruby on Rails. I'm an
enterprise .NET developer by day, but I'm trying to be a rails developer
by night. I say trying, not because I don't know rails, but because
their documentation sucks. Sure, there are plenty of tutorials for
beginners, maybe some for intermediate developers. They are spread out
across the internet in a haphazard way. Mostly blog posts showing
something cool they found out by perusing the rails codebase or by word
of mouth. So their documentation sucks, but I believe it's something
deeper. Maybe your API sucks.

<!--more-->

If you're looking for a long post on how
much rails API sucks, you're going to be sorely disappointed. Remember,
I do like rails. It's an easy framework for anyone to get into. If
you're looking to build simple
[CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
applications, rails is hugely productive. Just a simple set of terminal
commands and you have a full working application. Hell, no code
required. The problem is that all the work is hidden by code generation.
Once you have to do anything out of the ordinary, your stuck looking up
the documentation.

Why is this so difficult? Because the API isn't all
that great. There are multiple ways to do everything. Without
consistency, it's a matter of memorization, and who has time to memorize
when work needs to be done. The problem is compounded when you add in
the multitude of [gems](http://en.wikipedia.org/wiki/RubyGems) into your
project. All of these work, as [black
boxes](http://en.wikipedia.org/wiki/Black_box). You just run random
commands and something happens. These commands are all different and you
hope you don't get them confused.

Just for a test, I looked up the new
"respond\_with" command on Google. The first link to actual
documentation is the seventh one, and that is with me looking up the
exact command. The documentation is just bad. I still have to look up
things every time I have my editor open. There are ways to avoid this,
though. We could use an editor with code completion, but doesn't that
just hide the underlying problem? What we really need is a better API.

Now, I'm picking on Rails a little bit, and that framework doesn't
deserve all the negativity alone. .NET has the same problems, but it's
hidden behind the "Visual Studio" facade. With
[intellisense](http://en.wikipedia.org/wiki/Intellisense) (code
completion), I can see the list of methods on a class and descriptions
of them at a simple control and space. I admit that I do this quite a
bit with new libraries.

If you designed your APIs with consistency in
mind, your users wouldn't need to constantly reference the
documentation. Focus on the language (as in spoken) of your API. Speak
it out loud and just listen for the sentences that come out. Are you
hearing coherent thoughts? Do each of the sentences from your classes
and methods sound like they come from the same paper? Your methods
define your sentences, your classes define your paragraphs, and your
namespaces define your pages.

You'll find out that when your API makes
sense to you, it will start to make sense to your users. Too many APIs
try to focus too much on functionality and ignore verbal cohesion.
Others go the opposite route and become overly verbose. (I'm looking at
you testing frameworks). There is a happy medium to be found.

Just remember, when your users are complaining about your documentation, they
are really complaining about your API.
