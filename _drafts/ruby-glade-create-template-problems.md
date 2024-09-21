---
id: 147
title: 'ruby-glade-create-template problems'
date: '2010-06-03T12:40:59+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=147'
permalink: '/?p=147'
original_post_id:
    - '147'
categories:
    - software
---

There’s a neat way of generating a Ruby desktop user interface from the Glade UI designer. Useful walk-throughs, available on the net include:

- [Linux GUI programming with Ruby – by Rob Rohan](http://www.youtube.com/watch?v=PXpwC1o5AcI)
- [Creating a GUI application using Glade and Ruby](http://xrob.wordpress.com/2007/04/20/creating-a-gui-application-using-glade-and-ruby/)

However, I had some problems getting it working in the latest Ubuntu version.

### Fix for Ubuntu Lucid Lynx (10.04)

1\. Make sure you’ve created a libglade project.

2\. Update the generated code

### Why the lack of recent activity?

Links on the net for this project all seem to date from roughly three years ago which surprises me because it seems very useful. It would be interesting to know why there was a flurry of interest at that time and so little since. Maybe this approach only works for toy projects. Maybe ruby-gnome got a little ragged, as is suggested in [this blog entry](http://www.culmination.org/2007/05/17/ruby-gtk2-development-with-ubuntu-feisty-fawn/). Maybe rubyists found a better toolkit, perhaps [shoes](http://shoes.heroku.com/)? Or maybe people just started preferring python for gui projects – I seem to have seen quite a few of those recently, e.g. [Gwibber.](http://gwibber.com/)