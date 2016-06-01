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

## sharding strategy
- DB Field chosing, it should chose the filed that lead to least SQL and code change, to make the access fall in `one database`, instead of multiple DBs, which result in high I/O and significant logic change. 
- Here is one practice
-- Get all SQL
-- Pick up top fields appear in `where` clause.
-- List break down from three categories
1. Single ID, i.e. userID=?
1. Multiple ID. i.e. userID in (?,?,?)
1. Not show

|Field*|* Single ID *|* Multiple ID *|* Not show|
userID | 120 | 40| 330
orderID | 60 | 80| 360
shopID | 15 | 0| 485
