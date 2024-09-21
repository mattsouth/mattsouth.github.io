---
id: 305
title: 'Async sinatra'
date: '2013-06-07T08:42:02+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=305'
permalink: '/?p=305'
original_post_id:
    - '305'
categories:
    - software
---

I’ve been working a little with Sinatra again and found that I had a long running call that could use some asynchronous love. So I searched around for some existing solutions and came up empty handed. These are my notes…

Requirement

My basic requirement was to be able define a get call so that it could start a long running process in the background and then return a response immediately. This [stackoverflow post captures the requirement](http://stackoverflow.com/questions/849331/how-to-run-a-basic-asynchronous-job-within-sinatra) perfectly. However neither of the two solutions suggested worked for me..

Possible solutions

Spork

sinatra-dj

sinatra-syncrony

Conclusion

In the end this stackoverflow answer did the job… http://stackoverflow.com/questions/5652749/start-some-process-and-then-redirect-back-even-though-process-is-still-running?rq=1

My current thinking is that I either delve into the spork code to see how it’s done and butcher what I can or man up and upgrade to a padrino app that can use delayed-job properly. To be continued….

Perhaps this should tell me that I have reached the limit of Sinatra and should be using something a little heavier, but

EDIT:  
It was something simple in the end:

http://stackoverflow.com/questions/5652749/start-some-process-and-then-redirect-back-even-though-process-is-still-running

Lesson learned! When you believe there is a simple answer there probably is, but you might have look hard to find it. I also looked at:

http://stackoverflow.com/questions/849331/how-to-run-a-basic-asynchronous-job-within-sinatra

http://stackoverflow.com/questions/9911566/run-background-process-in-sinatra