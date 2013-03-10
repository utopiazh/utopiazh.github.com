---
layout: post
title: "Multi-tenant of HBase in FaceBook"
date: 2013-03-10 09:24
comments: true
categories: hbase, hadoop 
---

# Overview

Watched the video for 2 times to get the main point, the highlights learned from this video is:

+ Use unique message id as ts to store into hbase
+ Use monitoring/reporting tools to know what exactly the access pattern is, while the app developers don't know either
+ Use underlying hashout solution to isolate traffic, instead of an optimistic solution of using table names.


# HBase adoption 

## Messages:

**Requirements:**

- Very high volume (9B+ msg, 90B r+w ops per day), 4.5 PB no compressed.
- Elasticity & auto-failover
- Strong consistency within a data centeer
- import large data set (old data)

**Schema:**

- 3 CF (actions, snapshot (cache), keywords (search))
- Use message id as timestamp, which leverage the 3rd dimension.
- Fast iteration on schema 
    - Action logs are single source of truth
    - Most data during schema iteration from snapshot  and keywords
    - Custom backup solution (action logs), which could be replayed on schema evolving.

## ODS (Operational Data Store)
- Schema: 3CFs, raw, hour, days
- MR job to move data to buckets
- Compaction tricks (leverage the time series to pick the right HFile to achieve more spatial locality)
- Separating HBase clusters and its backing HDFS clusters proved not feasible
- HA is essential (Master/Master cluster replication with MR jobs)


# HBase best practices

**Process:**

Select the right apps: no five nines, etc.

Shadow testing before going production (real traffic goes in and out without noticed by users).

**Schema Design**

One CF or Multiple CF: common issue is putting all data into one CF, so get poor spatial locality 

New table or New CF: New CF provides better locality, e.g. users message and search, the best user experience is that all users data is complete available or down

**Lessons:**

- Need graph/reporting monitoring to provide insights
- Constant upgrade (facebook is running HBase 0.89 with back-ported patches)


# Multi-Tenants
**optimistic multi-tenancies**

- let users do the right things
- lack of table naming rules

**Hashout:**

- Was for Mysql, ported to support HBase
- review every app
- block abusive users, promote heave users
- users must provide app id and key, system app id to specific shard
- backed reading ops with memcached
- intensive MR job on separate cluster

# Reference

+ [Nicolas Spiegelberg - Multi-tenant HBase Solutions at Facebook](vimeo.com/44715953 "Multi-tenant HBase Solutions at Facebook")
