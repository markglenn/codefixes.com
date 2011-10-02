---
author: markglenn
layout: post
slug: nuget-and-what-we-can-learn-from-bundler-part-1
status: publish
title: NuGet and what we can learn from Bundler, Part 1
categories:
- .NET
- General
---

The new kid on the block in the .NET world is a package management tool
from Microsoft named [NuGet](http://nuget.codeplex.com/) (previously
NuPack). I'm excited to see Microsoft getting into this game since I've
noticed a lot of my projects have been heavily dependent on third party
libraries. My normal process for handling these dependencies is to
create a library directory and put all the DLLs that I need in there.
This worked fine for simple projects, but became complex when I had
multiple projects with interdependencies. In those cases, I had to make
sure that each of the third party DLLs were the same version for both of
the projects, or I created a external subproject in mercurial that
hosted the main DLLs. 

<!--more-->

In comes NuGet/NuPack. This really got me excited
since I had been accustomed to packaging systems such as [ruby
gems](http://rubygems.org/) and Debian's
[aptitude](http://en.wikipedia.org/wiki/Aptitude_(software)). I can now
pick and choose which third party assemblies I want, and have it install
everything automatically. It also handles the dependencies and upgrades
as needed. I can just choose NHibernate.Core, and its insurmountable
dependencies are pulled in for me.

[![image](http://www.codefixes.com/wp-content/uploads/2010/11/nuget-screenshot1-300x168.png "nuget screenshot")](http://www.codefixes.com/wp-content/uploads/2010/11/nuget-screenshot1.png)
Once I clicked the install button, NHibernate and all its dependencies
were cleanly added to my project, and a nice little *packages.config*
file was added with the following content:

``` xml
<?xml version="1.0" encoding="utf-8"?\>
<packages\>
  <package id="log4net" version="1.2.10" /\>
  <package id="Iesi.Collections" version="1.0.1" /\>
  <package id="Antlr" version="3.1.1" /\>
  <package id="Castle.Core" version="1.1.0" /\>
  <package id="Castle.DynamicProxy" version="2.1.0" /\>
  <package id="NHibernate.Core" version="2.1.2.4000" /\>
</packages\>
```

Of course, the configuration files weren't
updated for NHibernate configuration (which can be complex to setup),
but this is most likely a packaging issue and not a problem with the
plugin. I'm hoping the team who put together the package will add some
example configuration.

Also, a nice addition is the *Package Manager
Console*. This is a PowerShell shell that you can use to install the
packages, in case you already know which to add. This seems faster to
me, a reformed console guy, but your mileage may vary. 

NuGet downloads
all the packages into your solution folder under "packages." These DLLs
are then added as local references in the project. You can add the
packages folder to version control to safely keep them with the project.
I was disappointed to see that the packages.config isn't automatically
checked at load. It would be nice to have these dependencies downloaded
automatically so we don't have to add the DLLs to version control. 

So
this gets me to my point about some features I see as currently lacking.
Now, please take my criticism with a pound of salt; NuGet is still early
alpha. I know this is not a bug free/feature complete release,
especially since I'm living on the
[edge](http://nuget.codeplex.com/releases/view/54662).

Bundler is a gem
manager for ruby, and has recently been included with the now released
ruby on rails 3.0. Using a simple Gemfile, bundler will install all the
dependent gems in their correct locations. It handles versioning and
what the .NET crowd would call strong names. So it's pretty obvious that
these two systems are trying to handle the same problem... dependencies.

Overall, I've found NuGet a great start in this field for the .NET
world. Most of everything worked out of the box. I had the occasional
hiccups with installs. For example, NLog would not install after playing
around with the package manager for a while. My guess is that the
caching of the dependencies into the "packages" folder broke something.
I didn't look too deeply into it yet.

In my next post I'll try going
feature by feature through both NuGet and Bundler to compare what each
does right and possibly what can be fixed. I'm a little upset I didn't
get to it this time around, but I was actually struggling with syntax
highlighting plugins for WordPress for an hour or so.
