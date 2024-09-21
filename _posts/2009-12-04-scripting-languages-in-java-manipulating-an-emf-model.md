---
id: 72
title: 'Scripting languages in Java &#8211; manipulating an EMF model'
date: '2009-12-04T14:53:02+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=72'
permalink: '/?p=72'
original_post_id:
    - '72'
categories:
    - software
tags:
    - java
---

![](http://media.xircles.codehaus.org/_projects/groovy/_logos/medium.png "Groovy logo")I’m currently attempting to embed a scripting engine into a Java application. The [Java Scripting API](http://java.sun.com/javase/6/docs/technotes/guides/scripting/index.html) means this exercise should be quite straightforward (at least to get something up and running) and there is a huge choice of script languages to choose from so one of them ought to match my requirements, right?

I’m taking baby steps while I explore the space of possible options. So far I’ve prototyped an expression evaluator that accepts data in the form of simple Java framework objects and allows boolean expressions to be evaluated over them. In today’s baby step I thought I’d try and manipulate some non-framework Java objects built with an [EMF](http://www.eclipse.org/modeling/emf/) model that I’m currently working on and two different scripting languages, [Groovy](http://groovy.codehaus.org/) and [Rhino](http://www.mozilla.org/rhino/). Groovy is a scripting language that has grown out of the Java community in response to Python and Ruby. Rhino is a Javascript engine implemented in Java from the Mozilla foundation that is bundled as the default scripting engine in the Java6 JDK. I got somewhere with Groovy but got completely stumped with Rhino because I just couldn’t load my custom classes.

## Groovy

First the success story. I fired up the groovy shell (groovysh) in the directory that contains my classes and got started straight away:

`<span style="color:green;">Groovy Shell</span> (, JVM: 1.6.0_15)<br></br>Type 'help' or 'h' for help.<br></br>-------------------------------------<br></br><strong>groovy:</strong>000> dec = new argkit.decision.impl.DecisionImpl()<br></br><span style="color:red;">ERROR</span> java.lang.NoClassDefFoundError: <span style="color:red;">org/eclipse/emf/ecore/EObject</span><br></br><strong>at</strong> java_lang_Runnable$run.call (<strong>Unknown Source</strong>)`

Oh, yeah, I needed to add the EMF classes to the classpath. I could do that by restarting the shell with the EMF jars included in the classpath or add them in directly…

`<strong>groovy:</strong>000> this.class.classLoader.rootLoader.addURL(new URL("file:///.../org.eclipse.emf.ecore_2.5.0.v200906151043.jar"))<br></br>===> null<br></br><strong>groovy:</strong>000> this.class.classLoader.rootLoader.addURL(new URL("file:///.../org.eclipse.emf.common_2.5.0.v200906151043.jar"))<br></br>===> null<br></br><strong>groovy:</strong>000> dec = new argkit.decision.impl.DecisionImpl()<br></br>===> argkit.decision.impl.DecisionImpl@5878d2 (name: decision0, caption: null)<br></br><strong>groovy:</strong>000> cand = new argkit.decision.impl.CandidateImpl()<br></br>===> argkit.decision.impl.CandidateImpl@b9132a (name: candidate1, caption: null)<br></br><strong>groovy:</strong>000> dec.candidates.add(cand)<br></br>===> true<br></br><strong>groovy:</strong>000> cand.status<br></br>===> UNKNOWN<br></br><strong>groovy:</strong>000> arg = new argkit.decision.impl.ArgumentImpl()<br></br>===> argkit.decision.impl.ArgumentImpl@ce796 (name: argument2, caption: null) (support: +)<br></br><strong>groovy:</strong>000> cand.arguments.add(arg)<br></br>===> true<br></br><strong>groovy:</strong>000> cand.status<br></br>===> RECOMMENDED<br></br><strong>groovy:</strong>:000> arg.support = argkit.decision.Support.AGAINST<br></br>===> -<br></br><strong>groovy:</strong>:000> cand.status<br></br>===> REJECTED<br></br><strong>groovy:</strong>:000> exit<br></br>`

Having told Groovy about the EMF jars my code depends on, I create a decision object with one candidate and watch the recommended status of the candidate change with the addition of an argument and it’s subsequent manipulation.

## Rhino

Then I fire up the equivalent for Rhino (jrunscript), this time remembering to include the EMF jars on the classpath, and start my shell:

`js> dec = argkit.decision.impl.DecisionImpl()<br></br>script error: sun.org.mozilla.javascript.internal.EcmaError: ReferenceError: "argkit" is not defined. (<STDIN>#1) in <STDIN> at line number 1<br></br>`  
Ah. This was an unexpected issue as argkit is definitely on the classpath. And there’s pretty much where I got to. Some digging lead me to this [bug report](http://bugs.sun.com/bugdatabase/view_bug.do;jsessionid=79c908a33f1af578ad9b9996ee1f?bug_id=6799015) for Java which suggests that the problem is with the non-standard top level domain name (TLDN) in my package and points the finger at Rhino. Adjusting my model (by setting .org as the TLDN) for this perplexing issue got me a little further…

`js> dec = org.argkit.decision.impl.DecisionImpl()<br></br>script error: sun.org.mozilla.javascript.internal.EcmaError: TypeError: [JavaPackage org.argkit.decision.impl.DecisionImpl] is not a function, it is sun.org.mozilla.javascript.internal.NativeJavaPackage. (#1) in  at line number 1`

Ummm, it’s a what?

`js> org.argkit.decision.impl.DecisionImpl<br></br>[JavaPackage org.argkit.decision.impl.DecisionImpl]`

It’s certainly not a Java Package. It seems to me that Rhino was really not cut for this particular use case.

## Conclusions

So to recap, I tried to use Groovy and Rhino to manipulate some non-framework objects, as the expressions in my scripting engine embedded app will need to range over custom state objects and Groovy beat Rhino hands down in terms of ease of integration with the custom code. Now, if only I could get the [Groovy plugin for Eclipse](http://groovy.codehaus.org/Eclipse+Plugin) to install, but that’s another story…