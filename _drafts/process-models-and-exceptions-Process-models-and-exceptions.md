---
id: 54
title: 'Process models and exceptions'
date: '2009-10-30T11:12:26+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=54'
permalink: '/?p=54'
original_post_id:
    - '54'
categories:
    - software
---

I’ve spent some time recently focussing on a process modelling framework. This is not the first time I’ve done this, and I strongly suspect it will not be the last. This essay reflects some thoughts I’ve had on this activity and focusses on the difficulty and importance of modelling exceptions in a process. It begins with a look at the sales process behind a process modelling tool.

**How process modelling tools are sold**

TODO: What are process modelling tools?

The majority of process modelling focusses on how to do something right and not what happens when your process goes wrong – the exceptions. This state of affairs reflects the sales process – in order to sell one of these systems you show a demonstration of a simple process that’s roughly aligned with your prospective client and make arguments of the form:

- look how easy it is to model your own processes!
- look how elegant the representation is!
- see how easy it is to integrate with your existing systems!

But then when you actually start to model your own process you find that the exceptions dominate and that actually it isnt easy or obvious to know where to stop modelling the things that can go wrong. Almost inevitably the representation stops being elegant any more.

I’ve seen this happen in many projects, large and small. The classic project in my experience runs something like this. The sales team pitches the solution, which is based around a single page UML activity diagram and some short time scales. Once the project is sold, the business analyst starts talking to the end users and builds a 20 page UML diagram – where the core process has only grown to 2 pages and the rest of the pages are the exceptions. The time scales for project implementation blow up and relations with the customer start to get really difficult.

So the point of this essay, assuming you’re interested in modelling processes, is to urge you to consider the exceptions “up front” in your process modelling. It’s hard but it’s important. Furthermore, if done right, this approach could win you customers, not confuse them, and give you back control over your project deadlines.

**What’s hard about modelling exceptions**

Modelling exceptions is difficult because  
it hides the details of the ideal model  
it’s difficult to know where to stop

It’s the classic problem of trying to model unknown unknowns.

A checklist of exceptions to look for…

Also it’s difficult to know where to stop modelling what could go wrong. and very tempting to model the exceptions as processes themselves (you have the hammer to do this…). actually this is where the value of employing professionals, people who’ve met similar problems several times before, can show itself.

**Some hope amid all this complexity for the sales team**

Isnt this a little pessimistic. difficult to sell.

Emphasise the power of sceptical thinking.

End users often worry that systems based around process modelling are designed to take away their autonomy. This is not a worry I share because  
increasing complexity needs taming  
the role of people is to cope with things when they go wrong, not when they go right.  
This last point is the crux. …

**Conclusions**

Think about exceptions upfront. Know that they are going to dominate your model and plan for this.