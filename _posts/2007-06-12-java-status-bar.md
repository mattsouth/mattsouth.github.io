---
id: 434
title: 'Java status bar'
date: '2007-06-12T10:42:27+00:00'
author: matt
layout: post
guid: 'https://halfdecentnet.wordpress.com/2007/06/12/java-status-bar/'
permalink: '/?p=434'
original_post_id:
    - '1'
categories:
    - software
---

This might save someone else a little bother. I’ve been building Java Swing demo’s in the last few months and one thing that has slowed me down is building a status bar. A status bar is the strip at the bottom of a window that contains useful information about the status of an application.

There is no standard swing control (container) to do this so you must roll your own. Searching for “java status bar” didnt get me very far. Initially I just used a JLabel, but this is too simple. I really wanted something with multiple recessed panels (as in the skype example). I considered using an unfloatable JToolBar but I dropped this idea because a toolbar’s default background doesnt look like a status bar and because its not easy to make the recessed panels this way. Finally I realised that the best way to build my status bar is to nest JPanels.

Now it’s a little tricky to get the status bar behaving correctly on resize, but if you use a GridBagLayout for your top level JPanel then it’s doable. However, a GridBagLayout is pretty horrible to use so I constructed two helper classes, StatusBar and StatusBarPanel to make things eaiser. A StatusBarPanel is simply a JPanel extended with two extra attributes: an integer panelWidth and a boolean fixedWidth. Thus you can define the width that you wish for your panel and whether or not it can stretch on resize. The StatusBar class also extends JPanel and has an array of StatusBarPanel objects. A StatusBar object configures the GridBagConstraints for you when you give it the array of panels.