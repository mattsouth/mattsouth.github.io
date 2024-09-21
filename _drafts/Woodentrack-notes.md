---
id: 316
title: 'Woodentrack notes'
date: '2013-07-18T14:20:22+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=316'
permalink: '/?p=316'
original_post_id:
    - '316'
categories:
    - software
---

Last year in a slow period I knocked up a[ javascript library for making wooden toy train designs](http://www.github.com/mattsouth/woodentrack) as a useful/interesting exercise. After getting some implicit feedback on it last week (somewhat baffled), I decided to review it, give it a spruce up and add some more explanation. It’s still barely a proof of concept but you can see the results [here](http://mattsouth.github.io/woodentrack/demo.html).

The next pieces of work (should I get the chance) will probably focus on finessing the API, i.e. “Create a track at the browser command prompt, attach a track painter and watch the drawn track change as you add/remove pieces and edit the track properties” and adding annotations to the free ends of track drawn in the DSL demo.

Useful refs:

1. [Crockford – Private members in javascript](http://javascript.crockford.com/private.html "Crockford - Private members in javascript")
2. [Mozilla Developer Network – details of the object model](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model)

There were quite a few challenges in this. First off, the maths, though “high school level” trigonometry, was quite intricate. Then getting to grips with SVG. Then detecting free ends arose as a clear requirement to aid users with the DSL and to enable analysis of a track.

planning.

stage 1. get something up and running

stage 2. finesse the model. Make it dynamic – i.e. not have to be redrawn manually after each change.

stage 3. build some nice tool support

stage 4. build some analysis into the tool support.

technical specs

Allow users to programatically and dynamically update a track

d3 vs raphael?

requirements

I wanted to be able to easily build train track layouts for virtual exploration. The two main use cases I had came down to two questions:

1. Can a train traverse the whole track?
2. What other designs can I make with these pieces?

And I wanted to do this in a visual way, so I started by creating a library for building visual train tracks. Also this allowed me to explore svg and dust off my javascript fu.

One observation I’ve found when doing this is that there are surprisingly few tracks that fit properly. Take for example the following track which is a variation of one of my examples:

t(290,50,0): JRB YRB 2S 2R S Sh 2R 2S JRB YRB 2S 2R S Sh 2R 2S  
1C: MLB 4R YLB 3Sh JLB 4R YLB 3Sh

If you draw this you will see that the tracksdont quite match up.

Criticisms. The model imposes a need for several versions of the same piece. This is potentially confusing.

Connections. One thing that I havent included in the model yet is the concept of male and female connectors which imposes quite a serious constraint on the model and requires the choice of pieces to be more considered.