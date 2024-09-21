---
id: 192
title: 'Sinatra + Microsoft SQL server ??'
date: '2010-09-21T12:45:24+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=192'
permalink: '/?p=192'
original_post_id:
    - '192'
categories:
    - software
---

After writing the last post I realised that I’d jumped too far into the deep end with Padrino and really needed to understand the underlying [Sinatra](http://sinatrarb.com) and [Rack](http://rack.rubyforge.org/) frameworks better before commenting any further.I found the opportunity today for doing just that. I needed to make a demo web application that listed items from a Microsoft SQL Server and demonstrate integration with a third party service. I had started using MS Visual Web Developer for this task but found it horribly slow to use and difficult to move beyond the boiler plate applications because the c# framework learning curve was as little too steep for a quick and dirty demo.

After spending a couple of days on this, I thought I’d look for an alternative and wondered if sinatra might be useful. Instinct told me that connecting to the db might be an enormous time sink, but these two articles suggested otherwise:

- <http://techwhizbang.com/2010/03/jruby-activerecord-jdbc-sqlserver/>
- <http://stackoverflow.com/questions/2853788/how-to-connect-to-sql-server-using-activerecord-jdbc-jtds-and-integrated-securi>

and indeed it turned out to be just the case. With [JRuby](http://jruby.org/), Sinatra and[ jTDS](http://jtds.sourceforge.net/) I was able to get my little app up and running on Windows within a day.