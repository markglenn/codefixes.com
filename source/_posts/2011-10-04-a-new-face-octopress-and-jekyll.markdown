---
layout: post
title: "A New Face - Octopress and Jekyll"
description: CodeFixes.com switches to octopress and jekyll
keywords: programming,jekyll,octopress,blog,wordpress
date: 2011-10-04 16:30
published: false
comments: true
categories: 
- General
---

If you've been reading this site in the past, you may have noticed a facelift.
This isn't just a facelift, but a complete rewrite of the blog software that
I use.  I used to be hosting this site on wordpress, but I found I was battling
the system too often and trying to find work arounds for the quirks.
Now this site is just a bunch of static HTML files that were nicely
generated using Octopress and Jekyll.  This should significantly improve
the speed of the site and allow me to write more often (with more code examples).
I'm also finally able to host on "the cloud" using Amazon's S3 service which
finally allows me to do automated deployments.  As an added bonus, it also 
increases my geek status.

<!--more-->

So what real benefit does this give me?  Well for one, I can write everything
offline in markdown format without worrying about some converter messing up
the formatting.  I also have more control over the styling and layouts of the
page and it greatly simplifies my setup.

## Markdown and SASS goodness

Creating posts using only HTML tags can be time consuming and error prone.  The
problem is you have to force yourself to a subset of HTML which may be removed
by the Wordpress editor anyway.  Instead I can now use markdown, which is a 
simplified markup language that can be converted for me automatically and safely.
I can also use SASS to drastically simplify my CSS code.

## No backend

The best part is that the Markdown is converted to static HTML files.  That's right,
there's absolutely no backend for this site now.  You're downloading HTML files I 
generated on my computer directly without worry about putting things properly in
databases.  That means I can't have downtime due to a database crash, and there's 
no way I can lose data due to database corruption.  No need to run multiple servers
to handle the separation.

It's also impossible to hack, to a degree.  The only point of attack is now the web
server which will always exist.  There's no need to worry about patching wordpress
anymore (which is still an ongoing battle) nor any other software.  I just let Amazon
worry about the server software and just worry about content.

## Version control that makes sense

As a software developer, I'm used to great version control systems that give me more
than just history.  I'm not storing the entire site in a github project.  Since 
markdown files are just files, I can do diffs, branches, merges, even cherry pickings.
You can't even start to think about doing these things in wordpress, especially without
some major modifications to the software.

If you're interested in my setup, you can go to my github repository and download the 
entire thing onto your computer.
