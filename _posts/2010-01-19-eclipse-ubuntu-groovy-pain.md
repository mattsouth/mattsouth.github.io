---
id: 110
title: 'Eclipse + Ubuntu + Groovy pain'
date: '2010-01-19T15:17:06+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=110'
permalink: '/?p=110'
original_post_id:
    - '110'
categories:
    - software
tags:
    - 'eclipse ubuntu'
---

A couple of days ago the [v2 Groovy Eclipse plugin was released](http://docs.codehaus.org/display/GROOVY/Groovy-Eclipse+2.0.0+New+and+Noteworthy), but sadly I’m still not able to use it on my Ubuntu desktop because of a fairly convoluted set of configuration problems.

The first is that the linux download of eclipse doesnt work very well in the latest version of Ubuntu (Karmic Koala). A [work around is described here](http://mou.me.uk/2009/10/31/fixing-eclipse-in-ubuntu-9-10-karmic-koala/) with further links to Ubuntu’s issuelist. But actually the work around is only a partial fix because Eclipse sometimes starts a copy of itself and, when it does, it ignores the work around. This affects me as I’m currently trying to develop plugins.

One alternative approach that has worked for me so far is to use the version of eclipse that’s in the Ubuntu repositories. However, this version wasn’t taken from the final release of the eclipse codebase and the groovy plugin install, which patches the JDT (Java Development Toolkit) [just wont install in this version](http://jira.codehaus.org/browse/GRECLIPSE-498).

So to use the groovy plugin it looks as though I’ll have to wait for Eclipse 3.5.2 (which is [due on February 29th](http://wiki.eclipse.org/Galileo_Simultaneous_Release#SR2)).