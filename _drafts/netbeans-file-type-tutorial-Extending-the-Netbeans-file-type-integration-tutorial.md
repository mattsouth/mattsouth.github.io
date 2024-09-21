---
id: 221
title: 'Extending the Netbeans file type integration tutorial'
date: '2012-04-17T10:49:45+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=221'
permalink: '/?p=221'
original_post_id:
    - '221'
categories:
    - software
---

![](http://netbeans.org/images_www/v7/nb-logo-frontpage-70.png "Netbeans 7 logo")

I’ve been looking at creating support for a new language in Netbeans this week. This seems to be an important use case for the Netbeans project and there’s a good tutorial page for it: http://platform.netbeans.org/tutorials/nbm-filetype.html. Aside from a couple of omissions, this tutorial is a straight forward, powerful story that’s well told. However, it leaves some loose ends that I’ll look at here.

At the end of the tutorial you have three different views of the content of a simple text document:

1. The document text
2. A tree representation of the contents
3. A visual representation of the contents

However these representations are not properly synchronised and only one of them is editable. For my language I want to use all three representations; I want them synchronised in real-time and I also want each view to be editable. This article discusses how to achieve this goals.

# Real-time Synchronisation

At the end of the tutorial the three representations are only synchronised when the document is first loaded. After this the text and visual view of the document are synchronised when it is saved but the tree view is never synchronised.

## Line-aware nodes and node-aware lines

In order to get the text part of the document synchronising with the node tree part of the document we need both to be aware of each other. To do this we add some extra structure to the nodes and then wire up some lookup events.

# Three editable representations