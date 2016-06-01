---
layout: default
title: Database sharding
---

# DB sharding in YHD

There are two solutions when DB becoming bottleneck in yihaodian. 

- Scale up
Upgrade Oracle DB, adding more CPU , Disk and memory to incrase I/O performance. This is for short term only.
- Scale out
Divide the order table to multiple DBs, which is support horizontal extension, for long term purpose.
