---
title: Recover database from missing NDF and LDF files
date: 2022-06-01T01:29:29.835Z
draft: false
categories: Disaster Recovery
author: YohJawa
comments: true
share: true
tags: sqlserver,disaster-recovery
---
A friend of mine has just facing some trouble regarding their servers, this include their SQL server which store tera bytes of their transaction, all of their database backups were lost, and they only managed to recover the MDF file of that database, and a couple of NDF files.

He called me and asked if I could help recover some of their data from those files and if possible to bring the database back online. I said I'm not sure but if he could give me a chance I could try. Since this database has missing some NDF files and even LDF files, I can't just attach that database back so here is what I did :

* Create new empty database with similar file name as the damaged database
* Set OFFLINE all of the missing NDF files on this new database
* Set this new database OFFLINE and delete all of it's file from disk
* Copy the MDF and NDF files from damaged database to new database directory
* Set this new database ONLINE
* Run DBCC CHECKDB with REPAIR_ALLOW_DATA_LOSS against this database in EMERGENCY mode