---
layout: post
title: "My Must Have Gems"
date: 2011-10-11 21:10
comments: true
categories: 
- rails
- programming
---
{% img right /images/blog/ruby-gem.png "Ruby Gems" %}

When you create a new rails project, there are a few gems that you require to even get started. While rails does have a lot built into itself to help start you off in creating  great applications, I find myself in need of a more complete starting point.  I've compiled a short list of my most commonly used gems in new rails projects.

<!--more-->
## [Devise](https://github.com/plataformatec/devise) - Authentication

Every one of my projects in rails has required some sort of authentication system.  I have not found a better solution than Devise. It seems like it's the de-facto standard for authentication in rails. Even if you want to use other external authentication systems, like Facebook or Twitter, there are plugins built for devise that handle these systems also.  It's a super simple installation process and even simpler to use. 

## [RSpec](http://rspec.info/) - Testing

This is just a personal preference.  Test::Unit or Minitest can be substituted for rspec, but I've gotten used to the DSL that rspec includes.  Plus I prefer its included mocking framework for those few times that I need to stub out a method call.

## [factory_girl](https://github.com/thoughtbot/factory_girl) - Test factories

While rspec does give me a full featured mocking/stubbing framework, I personally prefer to use real objects for tests.  However, building objects using standard ruby methodologies can be time consuming and verbose, especially when you have hierarchical models. Factory girl simplifies this with a small DSL that allows me to define model factories one time while still allowing me to change them per test.  

The standard still used in rails is to use fixtures, but I feel that fixtures takes away part of the meaning of the test since it is separated in a different file.  Plus you have to know what exists in the fixtures before hand to make sure your tests are valid.  Instead, I can start with a clean slate for every test and define the model instances as they are needed, and define the exact parameters that are needed for that test instance.

## [Guard](https://github.com/guard/guard) - Automation

While not the first automated testing system, it is my favorite.  Using its plugin architecture, I can have it tests for files that have just been updated, start up my spork server, and restart pow as needed.

I also install gems to allow guard to notify me using Growl whenever events occur.  This is probably the nicest feature of guard which allows me to keep my eyes on the code without having to flip to the terminal all the time to run my tests.  That plus the speed of spork allow me to breeze through the code in no time.

## [Pry](https://github.com/pry/pry) - REPL and Debugger

If you are running ruby 1.8.7 or newer and haven't tried pry, you are really missing out on a great REPL system and debugger. On top of the standard read, execute, print loop, it allows you to also use ls and cd to browse through objects.  I use this to replace IRB in all my new rails projects and I've never been happier.  Ryan Bates has a great screencast on [RailsCasts](http://railscasts.com/episodes/280-pry-with-rails) about how to set this up.

## [Haml](http://haml-lang.com/) - Template Engine

When it comes to view engines, you have a few to choose from.  Rails comes standard with erb, but I prefer to use Haml. While some people may not like the limitations that come with Haml, I find the single line definitions force me to simplify my views significantly. I also like the simple syntax and the conciseness to the template language.  After working with HTML and XML for so long, it's nice to see how little code is required to do the same thing.

Of course, Haml does use indentation rules similar to Python and CoffeeScript. This can be a major turn off to some users. If you keep your views simple and extract partials wherever it seems reasonable, the indentation shouldn't be more than three or four layers deep.

## [Capybara](https://github.com/jnicklas/capybara)

Regression and full stack testing can be difficult without the right tools.  Luckily we have Capybara to handle a lot of the backend work to call into our server.  What we need to code is CSS or XPath selectors like you would using jquery. Add in a few automated input handling through the Capybara gem and you can easily  run through multiple pages in only a handful of lines.  This helps a great deal because it takes a lot of headaches of integration tests, making it more likely that I will write them more often.

## Summary

As I had [written before](/2011/10/how-rails-won-me-over/), one of the greatest assets that the rails community has is its vast collection of ruby gems. I have not seen another community release as many of these projects in such a relatively short amount of time.  Take advantage of some of these and you will find that you are much more productive and have fewer errors because you will have to write much less code and use more production tested gems. 
