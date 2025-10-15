---
title: Cluster Configuration
type: docs
layout: monstera
---

Monstera cluster consists of multiple **applications**. The framework does not know anything about applications except
of their names.

Each application core is defined on a keyspace `[0x00000000; 0xffffffff]` (4 bytes key). This keyspace is 
divided into **shards**. Division can be arbitrary, but typically follows powers of 2. For example, originally there
were 16 shards, then one of them grew and was split into halves. Now there are 17 shards: 15 of the size 1/16th of the
keyspace (`[0x00000000; 0x0fffffff]`, `[0x10000000; 0x1fffffff]`, and so on) and 2 of the size 1/32nd of the keyspace.
There should be no gaps between shards nor overlaps. Shards are referred by ids which are unique across the whole 
cluster. Theoretically, up to 2^32 shards per application is possible.

Each application has a configurable replication factor, which defines the minimum number of **replicas** for each shard.
Replicas are also referred by unique ids. Replicas are assigned to **nodes**. Each node is referred by an address of its
Monstera server including port (that allows to run several nodes on a single machine for development purposes). Two 
replicas of the same shard cannot be assigned to the same node. Replicas are assigned to nodes at creation and cannot be 
moved.

The whole cluster is defined by `ClusterConfig` which consists of all applications, shards, replicas, and nodes. It is
distributed as a single file to all nodes and clients. Processes or entire hosts can restart/reboot and still have 
access to the cluster config. New config is **pushed** to all nodes when it is changed. Cluster configuration does not 
change often, it can take weeks or months until there is a need to split a shard or move shards to new nodes. The diff
is always small, incremental, and safe to gradually rollout. That means that it is safe to have an old version of the 
config on some nodes in the cluster and a new version on others.  

Here is an example of `cluster_config.json` file:

```json
{
  "applications": [
    {
      "name": "Buckets",
      "implementation": "Buckets",
      "shards": [
        {
          "id": "Buckets_00_0f",
          "lower_bound": "00",
          "upper_bound": "0f",
          "replicas": [
            {
              "id": "Buckets_00_0f_b2acb652",
              "node_address": "ip-10-0-10-63.us-west-2.compute.internal:7000"
            },
            {
              "id": "Buckets_00_0f_4322c41c",
              "node_address": "ip-10-0-10-78.us-west-2.compute.internal:7000"
            },
            {
              "id": "Buckets_00_0f_3c877939",
              "node_address": "ip-10-0-10-14.us-west-2.compute.internal:7000"
            }
          ]
        },
        {
          "id": "Buckets_10_1f",
          "lower_bound": "10",
          "upper_bound": "1f",
          "replicas": [
            {
              "id": "Buckets_10_1f_7c1aedef",
              "node_address": "ip-10-0-10-14.us-west-2.compute.internal:7000"
            },
            {
              "id": "Buckets_10_1f_c64fa750",
              "node_address": "ip-10-0-10-63.us-west-2.compute.internal:7000"
            },
            {
              "id": "Buckets_10_1f_a4944668",
              "node_address": "ip-10-0-10-78.us-west-2.compute.internal:7000"
            }
          ]
        },
        //...
      ],
      "replication_factor": 3
    }
  ],
  "nodes": [
    {
      "address": "ip-10-0-10-78.us-west-2.compute.internal:7000"
    },
    {
      "address": "ip-10-0-10-14.us-west-2.compute.internal:7000"
    },
    {
      "address": "ip-10-0-10-63.us-west-2.compute.internal:7000"
    }
  ],
  "updated_at": "1750710750467"
}
```