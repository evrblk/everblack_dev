---
title: Cluster Configuration
type: docs
layout: monstera
---

Monstera cluster consists of multiple **applications**. The framework does not know anything about applications except
of their names.

Each application core is defined on a keyspace `[0x00000000; 0xffffffff]` (4 bytes). This keyspace is 
divided into **shards**. Division can be arbitrary, but typically follows powers of 2. For example, originally there
were 16 shards, then one of them grew and was split into halves. Now there are 17 shards: 15 of the size 1/16th of the
keyspace (`[0x00000000; 0x0fffffff]`, `[0x10000000; 0x1fffffff]`, and so on) and 2 of the size 1/32nd of the keyspace.
There should be no gaps between shards nor overlaps. Shards are referred by ids which are unique across the whole 
cluster. Theoretically, up to 2^32 per application shards is possible.

Each application has a configurable replication factor, which defines the minimum number of **replicas** for each shard.
Replicas are also referred by unique ids. Replicas are assigned to **nodes**. Each node has an id and an address of its
Monstera server including port (that allows to run several nodes on a single machine for development purposes).

The whole cluster is defined by `ClusterConfig` which consists of all applications, shards, replicas, and nodes. It is
distributed as a single file to all nodes and clients. Processes or entire hosts can restart/reboot and still have 
access to the cluster config. New config is **pushed** to all nodes when it is changed. Cluster configuration does not 
change often, it can take weeks or months until there is a need to split a shard or move shards to new nodes. The diff
is always small, incremental, and safe to gradually rollout. That means that it is safe to have an old version of the 
config on some nodes in the cluster and a new version on others.  

## Operations

Replicas are assigned to nodes at creation and cannot be moved. To move data from one node to another:

* Create a new (4th) replica on the target node.
* Wait until the new replica has caught up with Raft log and healthy.
* Remove the old replica from the source node.

This might be needed when:

* The total data/load on a given node is growing and some replicas should be moved out to reduce that.
* The node itself should be migrated (to a different location or to a larger instance size), so that all replicas should
  be moved out.
* A shard was recently split and one of the new halves should be moved out.

__TODO__
