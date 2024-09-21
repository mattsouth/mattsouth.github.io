---
id: 374
title: 'ipad/html5 date of birth input field'
date: '2014-02-12T14:22:08+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=374'
permalink: '/?p=374'
original_post_id:
    - '374'
categories:
    - software
---

Playing around with usability for an html5 date of birth input field today. Mixed ability audience – general public on the iPad. Surprisingly difficult. Options include:

&lt;input type=”date”&gt;  
which works but gives you different widgets on different browsers (todo: screenshots)

&lt;input type=”text” placeholder=”DD/MM/YYYY”&gt;  
the placeholder is a good hint but clicking in this input goes to a text keyboard, not the numeric keyboard

&lt;input type=”text” pattern=”d\*” placeholder=”DD/MM/YYYY”&gt;gives you numeric keyboard but invalidates your input on adding the slashes

&lt;input type=”number” placeholder=”DD/MM/YYYY”&gt;

https://developer.apple.com/library/safari/codinghowtos/Mobile/UserExperience/\_index.html#//apple\_ref/doc/uid/DTS40008248-CH1-DontLinkElementID\_14

http://stackoverflow.com/questions/3090369/disable-validation-of-html5-form-elements