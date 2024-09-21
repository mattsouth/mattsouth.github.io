---
id: 248
title: 'Netbeans Navigation Window'
date: '2012-04-17T13:01:50+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=248'
permalink: '/?p=248'
original_post_id:
    - '248'
categories:
    - software
---

[Previously](http://halfdecent.net/2011/11/30/netbeans-file-type-integration-tutorial-comments/) I critiqued the [Netbeans File Type Integration tutorial](http://platform.netbeans.org/tutorials/nbm-filetype.html) suggesting that it ought to show how to implement a navigation window and that the various views ought to be synchronised in real-time. Since then I’ve looked at the work involved in implementing these suggestions and this blog entry walks through the first of these issues. It will show how to implement a view of the example abc file type in a navigation window, how to show properties of sub-nodes of the abc file and how we can move easily from the tree view of the abc-file type to the editor view. I am new to this framework so although I will walk through my rationale with references and working code (for Netbeans 7.1), my way may not be the best way. Please correct me if you see something you think could be achieved more elegantly / with less code / in a way that’s more in keeping with the current Netbeans RCP design principals and doesnt break obvious use cases etc.

# How to add a navigation window

The [Navigation API documentation](http://bits.netbeans.org/dev/javadoc/org-netbeans-spi-navigator/architecture-summary.html) is very clear – some of the easiest of the framework to read and includes useful examples. Following the “Basic Usage steps” I was able to get a navigator window up and running very quickly. I created two new classes, AbcNavigatorPanel and AbcNavigatorPanelUI, copy and pasting the example code provided. All I needed to do was update the constants at the top of the class as shown below:

```
public class AbcNavigatorPanel implements NavigatorPanel {
  /** holds UI of this panel */
  private AbcNavigatorPanelUI panelUI;
  /** template for finding data in given context.
  * Object used as example, replace with your own data source, for example JavaDataObject etc */
  private static final Lookup.Template MY_DATA = new Lookup.Template(AbcDataObject.class);

  //...
}
```

and then add a new folder to my layer file:

```
TODO: cut and paste from code and then dont use visual editor in wordpress
```

So now when I run the module and click on an abc file in the explorer or open in the editor then the navigator is populated with the explorer node tree. When I click on another file, the node tree is replaced by that file’s navigator structure.

# Linking sub-nodes to the editor

Clicking nodes in the navigator window should bring the cursor in the main editor window to the appropriate line of code. To link the sub-nodes of the navigator to lines in the editor we need to know the line number of the sub-node and use a line-cookie. For this we create a new class, AbcLineNode:

```
package org.myorg.abcfiletype;

import javax.swing.Action;
import org.openide.nodes.AbstractNode;
import org.openide.nodes.Children;

/**
 * An openide node representing a line in an abc-file.
 *
 * @author matt
 */
public class AbcLineNode extends AbstractNode {
    private int lineNumber=-1;
    private AbcDataObject dataObject = null;

    public AbcLineNode(AbcDataObject dataObject, String text, int lineNumber) {
        super(Children.LEAF);
        this.dataObject = dataObject;
        this.lineNumber = lineNumber;
        setDisplayName(text);
    }

    public int getLineNumber() {
        return this.lineNumber;
    }

    public void setLineNumber(int lineNumber) {
        int old = this.lineNumber;
        firePropertyChange(PROP_NAME, old, lineNumber);
        this.lineNumber = lineNumber;
    }

    public AbcDataObject getDataObject() {
        return this.dataObject;
    }

    private AbcLineNodeAction lineNodeAction=null;

    @Override
    public Action getPreferredAction() {
        if (lineNodeAction==null) {
            lineNodeAction = new AbcLineNodeAction(this);
        }
        return lineNodeAction;
    }
}
```

And then create a slightly different implementation for AbcNode children

```
public class AbcChildren extends Children.Array {
    private final AbcDataObject dObj;

    public AbcChildren(AbcDataObject dObj) {
        this.dObj = dObj;
    }

    @Override
    protected Collection initCollection() {
        Collection lines = new ArrayList();
        FileObject fObj = dObj.getPrimaryFile();
        try {
            int i = 0;
            for (String line : fObj.asLines()) {
                lines.add(new AbcLineNode(dObj, line, i++));
            }
        } catch (IOException ex) {
            Exceptions.printStackTrace(ex);
        }
        return lines;
    }

    private void updateNodes() {
        remove(getNodes());
        add(initCollection().toArray(new Node[]{}));
    }
}
```

And move the AbcChildren inner class from AcDataNode to a class of its own. Also in AbcDataObject we need to change the way the delegate node is constructed:

```
    @Override
    protected Node createNodeDelegate() {
        return new AbcNode(this, new AbcChildren(this), getLookup());
    }
```

In the previous version of AbcChildren we used a vanilla AbstractNode. Now we’ve subclassed it to create AbcLineNode which knows it’s original line number and we’ve also changed the way that the sub nodes are created (we’ve removed the AbcChildrenFactory from AbcDataObject) so that there isnt the possibility of the same node being used twice (which was possible before with the ). If we run the module again then it should work as before. To link the sub-nodes to the editor window we follow the hint from [Geertjan Wielenga](http://blogs.oracle.com/geertjan/entry/org_openide_cookies_linecookie) and create a new class, AbcLineNodeAction:

```
import java.awt.event.ActionEvent;
import javax.swing.AbstractAction;
import org.openide.cookies.LineCookie;
import org.openide.text.Line;

public final class AbcLineNodeAction extends AbstractAction {

    private final AbcLineNode context;

    public AbcLineNodeAction(AbcLineNode context) {
        this.context = context;
    }

    public void actionPerformed(ActionEvent ev) {
        AbcDataObject dobj = context.getDataObject();
        LineCookie lc = dobj.getCookie(LineCookie.class);
        Line line = lc.getLineSet().getOriginal(context.getLineNumber());
        line.show(Line.ShowOpenType.OPEN, Line.ShowVisibilityType.FRONT);
    }
}
```

Now when we run the module, and double-click on an abc sub-node the relevant line in the abc text file will be selected. Also if the file isnt open, it will be opened so that the line can be selected.

# Only show sub-nodes in the navigation window

At this stage we’re being shown the node tree of an abc file in the project explorer and the navigation window. This is overkill – we only need to show the tree in the Navigation window. To remove the sub nodes from the project explorer, remove the createNodeDelegate method from the AcbDataObject class.

TODO: fix the problem that doing the above means that we lose the custom properties dialogue.

# Linking sub-nodes to the properties window

TODO: Clicking nodes in the navigation window should change the context of the properties editor.