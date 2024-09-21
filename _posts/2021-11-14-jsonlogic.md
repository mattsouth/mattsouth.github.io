---
title: JsonLogic
date: '2021-11-14T22:08:00+00:00'
author: matt
layout: post
permalink: '/json-logic/'
categories:
    - software
---

I took a reasonably deep dive into [JsonLogic](https://jsonlogic.com) recently, evaluating it as a possible drop-in replacement for expression evaluation in [proformajs](https://gitlab.com/openclinical/proformajs). In the process I got my hands dirty with [vue3](https://vuejs.org) and [bootstrap5](https://getbootstrap.com) to create a JsonLogic [sandbox](https://mattsouth.github.io/json-logic-vue/?expr=!flag&context=%5B%7B%22name%22%3A%22flag%22%2C%22values%22%3A%5Bnull%2Cfalse%2Ctrue%5D%7D%5D) along with a [library](https://github.com/mattsouth/json-logic-to-js) for serialising JsonLogic expressions that maybe useful.

The library is indeed a suitable drop-in but the evaluation process has made me think twice of leveraging javascript expression semantics. Though it was a prudent time saving strategy at the time it was made, it may need reviewing.
