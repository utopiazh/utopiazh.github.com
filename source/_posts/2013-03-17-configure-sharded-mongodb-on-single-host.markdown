---
layout: post
title: "Configure Sharded MongoDB on single host"
date: 2013-03-17 10:54
comments: true
categories: mongodb 
---

The default configuration of mongodb only use a single thread, which will be
bottleneck.


## Config and Start mongodb

Start 3 config server
    mongod --configsvr --dbpath /var/lib/mongodb/configdb/27019 --port 27019 --logpath /var/log/mongodb/mongod-27019.log --logappend &
    mongod --configsvr --dbpath /var/lib/mongodb/configdb/27119 --port 27119 --logpath /var/log/mongodb/mongod-27119.log --logappend &
    mongod --configsvr --dbpath /var/lib/mongodb/configdb/27219 --port 27219 --logpath /var/log/mongodb/mongod-27219.log --logappend &

Start 3 data server
    mongod --dbpath /var/lib/mongodb/datadb/27029 --port 27029 --logpath /var/log/mongodb/mongod-27029.log --logappend &
    mongod --dbpath /var/lib/mongodb/datadb/27129 --port 27129 --logpath /var/log/mongodb/mongod-27129.log --logappend &
    mongod --dbpath /var/lib/mongodb/datadb/27229 --port 27229 --logpath /var/log/mongodb/mongod-27229.log --logappend &

Start mongos server

    mongos --configdb 127.0.0.1:27019,127.0.0.1:27119,127.0.0.1:27219 --port 27017 --logpath /var/log/mongodb/mongos-27017.log --logappend &

## Add shard for standalone mongod

Connect to mongos
    
    # mongo
    MongoDB shell version: 2.0.6
    connecting to: test
    mongos> sh.addShard("127.0.0.1:27029")
    mongos> sh.addShard("127.0.0.1:27129")
    mongos> sh.addShard("127.0.0.1:27229")

Enable shard for DB

    mongos> sh.enableSharding("github")

Create Index on the to-be-sharded key

    mongos> use github 
    mongos> db.repos.ensureIndex({"id" :1})

Enable shard for collection

    mongos> sh.shardCollection("github.repos", {"id": 1})

