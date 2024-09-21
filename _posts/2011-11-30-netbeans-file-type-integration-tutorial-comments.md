---
id: 228
title: 'Netbeans file type integration tutorial comments'
date: '2011-11-30T15:43:58+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=228'
permalink: '/?p=228'
wp-syntax-cache-content:
    - ''
original_post_id:
    - '228'
categories:
    - software
tags:
    - java
---

![](http://platform.netbeans.org/images/articles/71/netbeans-stamp.png)Netbeans 7.1rc1 has been released. When I went through the [file type tutorial](http://platform.netbeans.org/tutorials/nbm-filetype.html) (which has been updated for 7.1) I found a couple of minor niggles which needed more than a couple of lines in a comment to express, hence this post. In Summary, it’s a good tutorial, but there a few rough edges that could be ironed out:

- A design bug in the properties window section,
- Missing the visual library api dependency,
- Excessive overiding the default action on file context menu,

and it would really benefit from some extensions, particularly:

- implementing a navigation window instead of a node tree under the file node,
- real-time synchronisation across all views.

Everything up until the “Creating features for Abc files” stage in the tutorial worked smoothly for me. This section also works if you follow the instructions carefully (pay attention though folks, I forget to set the content type in the wizard when I did it). There are some misleading statements though, probably left over from earlier versions. In the first paragraph the introduction says “we enable the file to open into a window, instead of into an editor” but this is not what the action does – it simply raises a modal dialogue window. The next paragraph, “Adding a context-sensitive Action” then says that the wizard will register the newly generated class in the layer file, however in this version of Netbeans this no longer happens. Another niggle I have is with the action that’s created. The tutorial suggests we make our action the default action, the action that’s used for a double-click. This is annoying to me as the double-click action should be “open file in editor” so in my version of this I choose a different location in step 3.

“Creating additional Multiview windows” works just fine. “Parsing the file” also works but it’s not an elegant solution. Nodes are created when the file is first opened but then if the file is changed in the editor, those nodes are not updated. Another niggle I have with this section is that I think it would be better if we saw the tree in a navigation window but I’m not sure how much code this involves.

The “Extending the Properties window” section has a design error in it. The code provided attempts to preserve the existing file properties but fails because the new default properties set has the same default name. I would suggest the following variation in the AbcNode class:

```
public static String SHEET_ABC_PROPERTIES = "abc properties";

@Override
protected Sheet createSheet() {
  Sheet sheet = super.createSheet();
  sheet.get(Sheet.PROPERTIES).setDisplayName(NbBundle.getMessage(AbcNode.class, "LBL_Abc_PROPERTIES_File"));
  Sheet.Set set = Sheet.createPropertiesSet();
  set.setName(SHEET_ABC_PROPERTIES); // default is Sheet.PROPERTIES
  set.setDisplayName(NbBundle.getMessage(AbcNode.class, "LBL_Abc_PROPERTIES_Abc"));
  sheet.put(set);
  set.put(new LineCountProperty(this));
  return sheet;
}
```

with the addition of two new strings in the Bundle file:

```
LBL_Abc_PROPERTIES_File=File Properties
LBL_Abc_PROPERTIES_Abc=Abc Properties
```

The Final “Creating Synchronised views” misses the vital information that you need to add the “Visual Library API” library in order to compile, but this wasn’t too hard to work out. It works fine but the two views are only synchronised when the file is saved and this isn’t what’s described in the text. This lack of real-time synchronisation is further exacerbated by the lack of any synchronisation with the node tree in the project explorer.

To conclude, aside from fixing the niggles I would really like to see a navigation window implementation and better synchronisation between the views, however I found the tutorial as it stands very useful. And of course it could be that the amount of code needed for my suggestions exceeds the word limit for one of these tutorials.