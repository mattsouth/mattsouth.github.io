---
title: 'Munin on Ubuntu'
date: '2016-05-24T15:22:02+00:00'
author: matt
layout: post
permalink: '/installing-munin-on-ubuntu/'
categories:
    - sysadmin
---

I like [munin](http://munin-monitoring.org/). It’s an old school pluggable server monitoring framework that suffices well for my current purposes. This week I installed it on a new ubuntu box and it wasnt as straight forward as I’d hoped so here are some notes

[These instructions](https://www.digitalocean.com/community/tutorials/how-to-install-the-munin-monitoring-tool-on-ubuntu-14-04) will get you up and running but you wont get the rather useful dynamic zoom behaviour on the graphs and you’ll have added an unnecessary level of indirection when you changed the web directory from /var/cache/munin/www /var/www/munin. To get the dynamic zoom you need the *fcgid* (fast cgi daemon) apache2 mod which in turn needs the *libapache2-mod-fcgid* package. Also you’ll need the *<span class="pl-s">libcgi-fast-perl</span>* package. With these installed you just need to make a couple of small adjustments to the provided apache config and you’ll be good to go. I’ve created an [ansible playbook](https://gist.github.com/mattsouth/001228b74744fffa9d95705913cfcf0c) to do this for you if that’s your thing.
