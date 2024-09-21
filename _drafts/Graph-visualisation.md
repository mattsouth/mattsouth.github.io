---
id: 132
title: 'Graph visualisation'
date: '2007-11-07T10:52:58+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=16'
permalink: '/?p=132'
original_post_id:
    - '16'
categories:
    - software
---

I’ve been using [Jung](http://jung.sourceforge.net/) to visualise graphs (networks of linked nodes, not charts) in Java over the last year or so. When I started doing this I looked at several graph and visualisation APIs ([JGraph](http://www.jgraph.com/), [GINY](http://csbi.sourceforge.net/)) and found Jung to be the best match for my requirements. I’ve been generally very pleased with it – in particular the core graph API seems strong and it’s enabled me to get up and running quickly. The development team have released version 2.0 this year. This version, currently in alpha, will allow a graph object to use generics in defining the node/edge class which seems like a sound idea to me – it will certainly save me further time/code in the future.

Other interesting looking graph visualisation tool kits are [yFILES](http://www.yworks.com/en/products_yfiles_about.htm) (this one isn’t free), [http://prefuse.org](http://prefuse.org/)[ ](http://processing.org/) and <http://processing.org/> but I haven’t yet tried the last two properly.