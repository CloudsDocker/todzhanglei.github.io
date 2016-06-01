---
layout: default
title: Database sharding
---

# DB sharding in YHD

There are two solutions when DB becoming bottleneck in yihaodian. 

- Scale up
Upgrade Oracle DB, adding more CPU , Disk and memory to incrase I/O performance. This is for short term only, high cost.
- Scale out
Divide the order table to multiple DBs, which is support horizontal extension, for long term purpose.


Orgional Oracle is replaced by multiple MySQL DB, supporintg one master and multiple slaves, supporitng segratation of read and write. Leveraging `MySQL built-in` Master-slave replication (SLA<1 second)

## sharding dimensions
- DB Field chosing, it should chose the filed that lead to least SQL and code change, to make the access fall in `one database`, instead of multiple DBs, which result in high I/O and significant logic change. 
- Here is one practice
-- Get all SQL
-- Pick up top fields appear in `where` clause.
-- List break down from three categories
1. Single ID, i.e. userID=?
1. Multiple ID. i.e. userID in (?,?,?)
1. Not show

|Field| Single ID | Multiple ID | Not show|
|:---| ---:| ---:| ---:|
|userID | 120 | 40| 330|
|orderID | 60 | 80| 360|
|shopID | 15 | 0| 485|

It's obviously we should chose userID for sharding. Hold on, this is just `static` analysis, we should conduct `dynamic` study as well, so list most executed SQLs, e.g. top 15 SQL (account to 85% of SQL calls), if we conduct sharding by user ID, 85% of those SQL will fall in single DB and 13% fall in multiple DB, and only 2% will scan all DB, so the performance is must better than sharding on other ID fields.

## sharding strategy
