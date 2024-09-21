---
id: 201
title: 'Locating images within jars with Bash'
date: '2011-07-13T15:27:21+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=201'
permalink: '/?p=201'
original_post_id:
    - '201'
categories:
    - sysadmin
---

I’ve been working with Netbeans in the last couple of days, and this post is an aide-memoir for one of the more onerous tasks I came across. I wanted to re-use netbeans icons, but they were difficult to locate. As usual [stackoverflow had some useful information](http://stackoverflow.com/questions/1500141/find-a-jar-file-given-the-class-name) and what worked for me was the following bash command:  
`me@laptop:~/Applications/netbeans-6.9$ find . -name '*.jar' -type f | xargs -i bash -c "jar -tvf {}| tr / . | grep "saveAs.png" && echo {}"<br></br>847 Thu Jun 10 15:50:16 BST 2010 org.netbeans.modules.profiler.actions.resources.saveAs.png<br></br>847 Thu Jun 10 15:50:16 BST 2010 org.netbeans.modules.profiler.resources.saveAs.png<br></br>./profiler/modules/org-netbeans-modules-profiler.jar<br></br>847 Thu Jun 10 15:50:16 BST 2010 org.netbeans.modules.profiler.docs.helppages.img.saveAs.png<br></br>./profiler/modules/docs/org-netbeans-modules-profiler.jar`  
Which you can use to locate all .png images by replacing the “saveAs.png” as simply “.png”. The same idea can be used for locating the module of a particular class, e.g.:  
`me@laptop:~/Applications/netbeans-6.9$ find . -name '*.jar' -type f | xargs -i bash -c "jar -tvf {}| tr / . | grep "SaveCookie" && echo {}"<br></br>1550 Thu Jun 10 15:36:04 BST 2010 org.netbeans.modules.versioning.diff.EditorSaveCookie.class<br></br>./ide/modules/org-netbeans-modules-versioning-util.jar<br></br>7462 Thu Jun 10 15:34:38 BST 2010 org.netbeans.modules.settings.SaveSupport$SaveCookieImpl.class<br></br>./platform/modules/org-netbeans-modules-settings.jar<br></br>295 Thu Jun 10 15:34:04 BST 2010 org.openide.cookies.SaveCookie.class<br></br>./platform/modules/org-openide-nodes.jar`  
From which it can be seen that the save cookie class is in the Nodes module.