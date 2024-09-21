---
id: 28
title: 'bibtex based paper cache'
date: '2008-03-10T13:02:51+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=28'
permalink: '/?p=28'
original_post_id:
    - '28'
categories:
    - idea
    - research
    - software
---

I store a whole load of papers in a directory on my laptop and locate an appropriate reference by browsing the directory, or using a free-text search engine (e.g. beagle, tracker, google desktop). I do this because it’s a pain to keep on finding a paper on the web and because I’m not always online and often I’m not in my office in the university, so encounter annoying pay-walls (which are not insurmountable, I could use ATHENS, but still, I think it’s a pain). Also, generally speaking, books and papers are not living documents; once published, they don’t change, so there is no risk in maintaining a local cache. This strategy kind of works. It’s principle strengths are it’s simplicity and scalability. It’s a little bit ugly though. The most ugly thing about it is that I can’t decide on a

file naming

additional info – urls, notes  
pros/cons

\+ simplicity

\+ scalability

– ugly

– extendability

This strategy kind of works. It’s principle strengths are it’s simplicity and scalability. But it’s also a bit ugly and begging for a little more structure. Bibtex could provide that structure. This is how it would work if I did this…

New Tool

I could build a tool that automatically populated my papers directory using the bibtex index and…

warned me if the link was no longer hot (after 3 missed tries perhaps?)

made a nice pdf index of all my real and virtual papers

If I included a bibtex file in my papers directory then I could also