---
id: 336
title: 'Snomed API'
date: '2013-08-21T22:47:49+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=336'
permalink: '/?p=336'
original_post_id:
    - '336'
categories:
    - software
---

Steps to use snomed api:

Download TRUD files – e.g. ftp://www.uktcdownload.nss.cfh.nhs.uk/15.0.1/NHS\_SNOMED/nhs\_snomed\_15.0.1\_20130401000001.zip (the large file in [ftp://www.uktcdownload.nss.cfh.nhs.uk/15.0.1/NHS\_SNOMED/](ftp://www.uktcdownload.nss.cfh.nhs.uk/15.0.1/NHS_SNOMED/))

clone project and create new eclipse project around it.

run loader

create table Concept (‘CONCEPTID’ PRIMARY KEY, ‘CONCEPTSTATUS’, ‘FULLYSPECIFIEDNAME’, ‘CTV3ID’, ‘SNOMEDID’, ‘ISPRIMITIVE’);  
Adding Concept data … done (19862 milliseconds)  
create table Description (‘DESCRIPTIONID’ PRIMARY KEY, ‘DESCRIPTIONSTATUS’, ‘CONCEPTID’, ‘TERM’, ‘INITIALCAPITALSTATUS’, ‘DESCRIPTIONTYPE’, ‘LANGUAGECODE’);  
Adding Description data … done (29346 milliseconds)  
create table Relationship (‘RELATIONSHIPID’ PRIMARY KEY, ‘CONCEPTID1’, ‘RELATIONSHIPTYPE’, ‘CONCEPTID2’, ‘CHARACTERISTICTYPE’, ‘REFINABILITY’, ‘RELATIONSHIPGROUP’);  
Adding Relationship data … done (308200 milliseconds)  
create index i1 on Relationship(CONCEPTID1); … done (51369 milliseconds)  
create index i2 on Relationship(CONCEPTID2); … done (26859 milliseconds)  
create index i3 on Description(CONCEPTID); … done (11847 milliseconds)  
create table Suffix (‘SUFFIXID’ PRIMARY KEY, ‘VALUE’); … done (1 milliseconds)  
create table ConceptSuffix (‘CONCEPTID’, ‘SUFFIXID’); … done (0 milliseconds)