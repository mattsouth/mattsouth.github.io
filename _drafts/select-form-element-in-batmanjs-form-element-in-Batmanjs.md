---
id: 382
title: 'form element in Batmanjs'
date: '2014-02-12T15:05:26+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=382'
permalink: '/?p=382'
original_post_id:
    - '382'
categories:
    - software
---

Today I was working on a batmanjs single page application with a nodejs backend. We were migrating the datastore from an rdbms to a nosql/document store solution.

```
class User extends Batman.Model
  @encode 'name', 'programme'

class Programme extends Batman.Model
  @encode 'name', 'category'
```

With the rdbms I have a controller that when creating a new user does something like this:

```
newUser = new MyApp.User
  programme: @get('programmes')[0].get('id')
```

and writes in the html form using jade templating like this:

```
form.form-horizontal
  .control-group
    label.control-label(for="user_Name")= t("user.name")
    div.controls
      input#user_Name(type="text",data-bind="newUser.name")
  .control-group
    label.control-label(for="user_Programme")= t("user.programme")
    div.controls
      select#user_Programme(data-bind='newUser.programme')
        option(data-foreach-programme="programmes", data-source="programme.name", data-source-value="programme.id", data-source-id="programme.id | prepend 'user_sel_Programme'
```

Which yields a select box that’s bound to the newUser.programme attribute as an integer. Thus when the form is first painted it selects the default first programme which you can change and the reflected change is fed straight back to the underlying newUser object.

But with the NOSQL backend we’re not passing IDs around anymore, we’re passing around objects so I tried to alter the template accordingly, however I couldnt for the life of me get it right.

So at the controller, when the newUser object is created we give it a default programme object, not ID i.e.

```
newUser = new MyApp.User
  programme: @get('programmes')[0]
```

And the ideal is that we set up the template so that the html binding knows that we’re selecting over a set of objects (i.e. the programmes).

The nearest I could get to was this:

```
form.form-horizontal
  .control-group
    label.control-label(for="user_Name")= t("user.name")
    div.controls
      input#user_Name(type="text",data-bind="newUser.name")
  .control-group
    label.control-label(for="user_Programme")= t("user.programme")
    div.controls
      select#user_Programme(data-bind='newUser.programme')
        option(data-foreach-programme="programmes", data-source="programme.name", data-source-value="programme", data-source-id="programme.id | prepend 'user_sel_Programme'
```

which works, in the sense that the correct programme is pre-selected and the programme is updated when you change the appropriate select option but the value on the programme attribute of the newUser object is now the programme name not the programme object. So now when we come to save our object we need to do a bit of fancy footwork, e.g.

```
newUser = @get('newUser')
programme = @get('allProgrammes').forEach (p) ->
  p if p.name == newUser.get('NewMonitoringProgramme')
newUser.set 'newMonitoringProgramme', programme
```

It would be much nicer if batmanjs could bind to the object.