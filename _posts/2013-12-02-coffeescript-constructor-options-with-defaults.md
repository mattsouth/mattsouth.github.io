---
title: 'Coffeescript constructor options with defaults'
date: '2013-12-02T12:05:52+00:00'
author: matt
layout: post
permalink: '/coffeescript-constructor-options-with-default/'
categories:
    - software
---

Coffeescript has a nice way of [destructuring assignment](http://coffeescript.org/#destructuring) in a class constructor, e.g.

```
class Person
  constructor: (options) ->
    {@name, @age, @height} = options
```

This is elegant and efficient and has the additional benefit of explicitly communicating anticipated class attributes, cf:

```
class Person
  constructor: (options={}) ->
    for key, val of options
      @[key] = val
```

which allows any old thing to be added to your object (although admittedly this is sometimes desirable).

Coffeescript also has a neat way of setting [default values for functions](http://coffeescript.org/#literals), e.g.

```
fill = (container, liquid = "coffee") ->
  "Filling the #{container} with #{liquid}..."
```

But this pattern doesnt seem to transfer to destructuring class assignment. I can’t for instance use any of these approaches:

```
class Person
  constructor: (options) ->
    {@name = "Ken", @age, @height} = options # (yields an "UNEXPECTED=" error) or
    {@name: "Ken", @age, @height} = options # (yields a "Ken" CANNOT BE ASSIGNED error)
    {@name ?= "Ken", @age, @height} = options # (yields an "UNEXPECTED COMPOUND ASSIGN" error)
    {@name? "Ken", @age, @height} = options # (yields an "UNEXPECTED LOGIC" error)
    {@name || "Ken", @age, @height} = options # (yields an "UNEXPECTED LOGIC" error)
```

It turns out that the best way (IMO) is:

```
class Person
  constructor: (options={}) ->
    {@age, @height} = options;
    @name = options.name ? "Ken"
```

Note that the default value for options is included, so as not to force a parameter on the constructor. As always, stack overflow [provides a deeper picture](http://stackoverflow.com/questions/11493163/deconstructing-a-list-of-parameters-in-class-constructor-coffeescript).
