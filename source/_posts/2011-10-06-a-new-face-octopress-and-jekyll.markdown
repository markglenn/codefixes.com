---
layout: post
title: "A New Face: Octopress and Jekyll"
keywords: programming,jekyll,octopress,blog,wordpress
date: 2011-10-06 16:30
published: true
comments: true
categories: 
- General
---

{% img right /images/blog/octopress_teaser.png "Octopress" %}

If you've been reading this site in the past, you may have noticed a face lift.
This isn't just a face lift, but a complete rewrite of the blog software that
I use.  I used to be hosting this site on wordpress, but I found I was battling
the system too often and trying to find work arounds for the quirks.
Now this site is just a bunch of static HTML files that were nicely
generated using [Octopress](http://octopress.org/) and [Jekyll](http://jekyllrb.com/).  
This should significantly improve the speed of the site and allow me to write 
more often (with more code examples).  I'm also finally able to host on "the cloud" 
using [Amazon's S3](http://aws.amazon.com/s3/) service which
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
by the Wordpress editor anyway.  Instead I can now use 
[markdown](http://daringfireball.net/projects/markdown/), which is a 
simplified markup language that can be converted for me automatically and safely.
I can also use [SASS](http://sass-lang.com/) to drastically simplify my CSS code.

Markdown, at least with the extensions brought in from Jekyll, has the benefit
of allowing me to insert code directly into the content.  I've struggled getting
code to properly format using Wordpress in the past, so this is a huge benefit.

## Uses ruby

As a new found ruby developer, I like the fact that Jekyll allows me to run 
arbitrary ruby code while generating the site.  For example, I use this to insert
the page links in the index pages.  I don't have to manually handle these
housekeeping issues by handing them off to an automated process.  The fact that
it's ruby is a bonus since this is what I work with daily.

## No back-end

The best part is that the Markdown is converted to static HTML files.  That's right,
there's absolutely no back-end for this site now.  You're downloading HTML files I 
generated on my computer directly without worry about putting things properly in
databases.  That means I can't have downtime due to a database crash, and there's 
no way I can lose data due to database corruption.  No need to run multiple servers
to handle the separation.

It's also much more difficult to attack the site.  The only point of attack is now the web
server which will always exist.  There's no need to worry about patching wordpress
anymore (which is still an ongoing battle) nor any other software.  I just let Amazon
worry about the server software and just worry about content.

## Automatic deployment

``` bash
$ rake s3deploy
```

That's all I have to do to push the new content live.  It's a great feeling.

### Offline access

One of the issues I ran into a lot was that my wordpress site could not be accessed
without an internet connection.  I spend a lot of time on the train to and from work
where I don't have access to the internet.  That means I could not see what the site
would look like while making changes during that time.  I'm sure I could have setup
a LAMP server locally to do development, but it was more work than I wanted to put into
it.

Instead, I can run the entire site locally by generating the site or running a rake
task to run a [WEBrick](http://en.wikipedia.org/wiki/WEBrick) server.  And, it will look 
and at exactly as I see it when I finally do deploy.  There are a few external
services that won't work, such as my twitter feed, but that's a minor issue
since I don't usually maintain that part of my site.

## Version control that makes sense

As a software developer, I'm used to great version control systems that give me more
than just history.  I'm now storing the entire site in a github project.  Since 
markdown files are just files, I can do diffs, branches, merges, even cherry pickings.
You can't even start to think about doing these things in wordpress, especially without
some major modifications to the software.

If you're interested in my setup, you can go to my 
[github repository](https://github.com/markglenn/codefixes.com) and download the 
entire thing onto your computer.  In the future, I may talk about how I set the site
up and my own customizations.
