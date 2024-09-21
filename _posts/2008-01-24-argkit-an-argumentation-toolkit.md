---
id: 24
title: 'ArgKit: An argumentation toolkit'
date: '2008-01-24T15:33:30+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/2008/01/24/argkit-an-argumentation-toolkit/'
permalink: '/?p=24'
categories:
    - software
---

[![ArgKit website](http://halfdecent.net/wp-content/uploads/2008/01/website.thumbnail.png)](http://www.argkit.org "ArgKit website")Last week I released an open source project: [ArgKit](http://www.argkit.org "ArgKit"). It’s the synthesis of some work that I’ve been doing in the last couple of years and I’m very pleased with it. I’ve released early (ish) on this one, so there is more work to come in the same vein, time and attention allowing. One thing that ArgKit’s website misses is some background on “what is argumentation?” so I thought I’d just blog something about Dungine – the only tool in the toolkit at the moment, based on an email I sent to a friend recently (thanks for the question Steve).

If you look at the [wikipedia argumentation entry](http://en.wikipedia.org/wiki/Argumentation), you’ll see that Dung is mentioned in the Artificial Intelligence (AI) section. The underlying model for Dungine, Dung’s acceptability semantics, is interesting to people who work in AI and are trying to capture how people reason and debate, particularly with inconsistent evidence and automate reasoning in this context. In my lab we use ideas like this to try and improve clinical decision support systems that:

- recommend diagnoses for a patient with a history and a set of symptoms and
- recommend treatments for a diagnosed condition.

Clinicians don’t always agree, and neither does the evidence upon which they base their opinions. If we can adequately represent their arguments, then this software might allow us to automatically reason about which of those arguments we should accept.

In the business world one might use Dungine to:

- accept a recommendation from a source on the web or
- represent a decision about granting a loan,

but there are many alternative approaches to supporting these examples, including Bayesian methods or applying a set of prioritised rules. My intuition is that argumentation is most useful in situations where it feels natural to represent contradicting reasons for doing something (accepting the recommendation or granting the loan) but this is a new area, and there are too few examples of it’s application in the wild. So I’ve built this library to help people give it go, and in doing so gather empirical evidence to help us understand where it’s a practical and useful technique.