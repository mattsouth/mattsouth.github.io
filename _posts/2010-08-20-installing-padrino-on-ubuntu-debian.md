---
id: 175
title: 'Installing Padrino on Ubuntu / Debian'
date: '2010-08-20T21:39:31+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=175'
permalink: '/?p=175'
original_post_id:
    - '175'
categories:
    - software
---

![](http://www.padrinorb.com/images/padrino.jpg "Padrino logo")

I’ve been tinkering with [Padrino](http://www.padrinorb.com) this week. Padrino is a ruby web framework built on top of the delightful [sinatra microframework](http://www.sinatrarb.com). I found it attractive because

- it appears to have a simple design, as you’d expect of something built on top of sinatra,
- it rolls in the various elements that you’d expect for a fully fledged web framework (i.e. orm, database, mailer) but makes no commitments to the particular modules used for each \*
- it had a default Admin interface (which is a huge win for Django IMO).

There’s quite a bit of supporting material on the web, but my impression after a few hours is that it’s still pretty beta and has a strong leaning towards RHEL linux. So this post details the steps I had to take to be able to work through the [basic project guide](http://www.padrinorb.com/guides/basic-projects) with Ubuntu Lucid Lynx.

For starters I couldnt use Ubuntu’s default version of rubygems, so I uninstalled it and installed the latest. This allowed me to apparently install the framework but there were still several hidden dependencies to uncover before I could walk through the guide.

I was able to generate a project but found lots of errors pointing to missing gems when I tried to create the in-built admin application. I found I had to install: rake, haml, rack-flash, thin, activerecord, sqlite3-ruby and datamapper gems and for sqlite3-ruby I needed libsqlite3-ruby and libsqlite3-dev via apt-get.

With these installed, when I attempted to create an admin app I wasnt getting errors, but it wasnt working:

me@laptop:~/padrino/first\_go$ padrino g admin  
=&gt; Located unlocked Gemfile for development  
Please specify generator to use (project, app, mailer, controller, model, migration)

Fortunately, [someone else had got there first.](http://groups.google.com/group/padrino/browse_thread/thread/74734c44c8a421b6) Installing libssl-dev and libopenssl-ruby through apt-get allowed me to generate an admin app. It’s cute and I’m able to do everything I’ve tried so far. I’m still getting “=&gt; Located unlocked Gemfile for development” messages when I interact with padrino which suggests something is up, but I haven’t worked out what it is yet or whether it’s something I need to worry about.

\* it remains to see if this approach is successful. It could be that maintaining agnosticism towards the various modules means that the API becomes too hard to use, but it’s certainly interesting to watch them give this a go.