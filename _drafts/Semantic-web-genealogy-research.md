---
id: 25
title: 'Semantic web genealogy research'
date: '2008-04-18T22:45:40+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=25'
permalink: '/?p=25'
original_post_id:
    - '25'
categories:
    - software
---

In recent years I have been given family trees by enthusiastic relatives which contain a lot of interesting data. On each occasion I have thought that publishing these data on the web would make a nice project. At the same time I have been trying to understand semantic web technologies. It seems obvious to me that the two exercises can be combined so I started a little project to create a web interface that understands family tree data. This project has two parts – the first is to identify the best representation for my data, and the second is a good web interface. This blog is mini report into part 1 – i.e. what is the best ontology to use for publishing my data and building my web interface. “Best” in this instance is a matter of balancing up a model that allows me to represent my data and at the same time re-use existing models (re-use is the point, right?).

**Requirements**

So the project is to publish my family tree on the web. Although I’m planning to use the semantic web which means that data model is infinitely extensible, I’m trying to re-use existing ontologies as much as possible. Thus, it helps to articulate the data I will be representing:

- name (mandatory),
- date of birth,
- married to relationship,
- child of relationship,
- Perry number (a number that indicates your separation from a key family member)
- Notes

Note that because of the nature of my source data, I’m not interested in date of death, date of marriage and date of divorce, but these are all things that I’m assuming should be captured in a genealogy ontology. Similarly there are certain derived relationships that I would expect to be representable, e.g. “parent of” and “sibling of”. Note also that I am not capturing the nice tree illustration, roots and all, from the original source material.

 **Genealogy models**

My first google search threw up a useful article [\[1\]](#1) with links to several more, notably [\[2\]](#1). Historically there have been several formal syntaxes for recording family trees. GEDCOM is the most used of these. GEDCOM started off as a text format, but there is an XML version and an OWL version in existence. GEDCOMs model uses events that are constrained with cardinality restrictions. For instance, a person can be born (an event) or die (an event) only once but can get married (an event) more than once. This model seems very sensible and allows for complicated things like adoptions and gender re-assignments to be modelled. However the standard implementation (http://www.daml.org/2001/01/gedcom/gedcom) seems unsatisfactory to me. It appears as if attributes are not connected to classes explicitly, but only implicitly through a inheritance structure that matches the class inheritance structure. This makes the model very difficult to reason over. Also the notion of a family is implemented, as a vehicle for holding family events (marriage and divorce), but this concept is not clearly defined.

 **Ontologies**

Ignoring the exercises A family tree is a classic AI/logic example so there are a bound to be a few toy examples that you just learn to ignore. Swoogle. http://protege.cim3.net/file/pub/ontologies/family.swrl.owl/family.swrl.owl http://orlando.drc.com/semanticweb/daml/ontology/Genealogy/Gentology-ont (found using a search for “geneaology” on swoogle)

**References**

1. <a name="1" title="1"></a>[Genealogy and the Semantic Web: A Guide for Family Historians and Amateur Genealogists](http://polaris.gseis.ucla.edu/mleahey/genealogyAndSemanticWebXHTML.htm)
2. <a name="2" title="2"></a>[The Semantic Web for Family History](http://jay.askren.net/Projects/SemWeb/)