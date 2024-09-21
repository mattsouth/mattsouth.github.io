---
id: 164
title: 'Potentially useful mysql bash scripts'
date: '2010-08-02T11:20:19+00:00'
author: matt
layout: post
guid: 'http://halfdecent.net/?p=164'
permalink: '/?p=164'
original_post_id:
    - '164'
categories:
    - sysadmin
---

Occasionally I put an admin hat on. These are a couple of useful scripts for your development / demo servers.

- [A script for backing up all your MySQL databases to file](http://halfdecent.net/2010/08/02/useful-mysql-bash-scripts/#backup)
- [Updating dates in a demo database refresh restore](http://halfdecent.net/2010/08/02/useful-mysql-bash-scripts/#daterefresh)

## <a name="backup"></a>A script for backing up your databases to file

In my experience it’s remarkably difficult to restore MySQL databases from the raw database files. On the other hand, it’s very easy to restore databases from a dump script. This bash script creates dump scripts for all your non-system mysql databases in a directory that can then be backed up every night. \[sarcasm\] It’s probably not appropriate for production servers.

```
#!/bin/sh
#A bash script that backs up each database into a sepearate file, database_name.sql

for i in `echo "show databases" | mysql -u backup -pbackuppassword`;
do
  if [ ! "$i" = "Database" ] && [ ! "$i" = "mysql" ] && [ ! "$i" = "information_schema" ]
  then
    mysqldump -u backup -pbackuppassword $i > /backup/mysql/$i.sql
  fi
done
```

Note that the success of this approach depends on you having a *backup* mysql user set up with the appropriate permissions for all databases.

## <a name="daterefresh"></a>Nightly restores of a demo database with updated dates

In one of our demos, we back our application with some demo entries and allow interested folk to play with those entries and create new ones. In order to maintain a sense of order in the demo database, it gets refreshed every night. Bash’s date manipulations can be useful here. Having restored the database, i.e.:

```
# step 1. clear database and add example patients
mysql -u mydbuser -pmydbuserpassword mydb < mydb.sql
```

We can tweak the dates to make the data seem fresh…

```
# step 2. update dates
mysql -u mydbuser -pmydbpassword mydb -e "update mytable set last_seen = '`date --date='1 day ago' '+%y-%m-%d %H:%M:%S'`'"
```

Note how the date program allows you to use natural language modifers like “2 weeks ago” to define your date.