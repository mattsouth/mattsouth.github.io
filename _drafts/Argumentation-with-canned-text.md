---
id: 20
title: 'Argumentation with canned text'
date: '2007-08-01T17:00:27+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=14'
permalink: '/?p=20'
original_post_id:
    - '14'
categories:
    - software
---

For the last few months I’ve been wrestling with argumentation based dialogue in the [ASPIC](http://www.argumentation.org) project. But over the weekend I thought I’d take a break and revisit something that was a bit half-baked in the inference engine – canned text. It’s come out quite well I think.

The inference engine uses a prolog-like language that I now call the “default knowledge syntax”. This syntax serves it’s purpose but has some flaws. It allows us to test and demonstrate the inference engine but it isnt very user friendly and it utilises a-priori weights for clauses that are difficult to justify in a principled manner.