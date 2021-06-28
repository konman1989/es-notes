## Replication

If a node's hard drive fails, the data is lost. The replication concept comes into play. It is a copy of an existing primary shard. There are two main reasons behind keeping replicas:

1. A replica shard can be promoted to a primary shard if the primary fails.
2. Get and search requests can be handled by primary or replica shards, so having replicas can improve performance.

* Replication is configured at the index level
* It works by creating copies of shards referred to as replica shards
* A shard that has been replicated is called a primary shard
* A primary shard and its replica shards are referred to as a replication group
* Replica shards are a complete copy of a shard
* A replica shard can serve search queries, exactly like its primary shard
* When creating an index we can choose how many replica shards we want

To prevent loosing all the data replica shards are never stored on the same node as their primary shard. 

### Example

If we have 1 node in the cluster and 2 shards with 1 replica for each, the replica shards will be unassigned. We now need to add an additional node to the cluster. Remember that theses nodes need to be on an independent hardware so ther is no single point of failure. Once ES recognizes that we have an additional node, it will enble replication.

* Typically you will be fine with one or two replicas but that depends on how critical the stored data is.
* For prod you will need at least 2 nodes to protect agains data loss.

## Snapshots

* ES supports taking snapshots as backups
* Snapshots can be used to restore to a given point in time
* They can be taken at the index level, or for the entire cluster
* Use snapshots for backups and replication for high availability (and performance)
* Replication is inded a way of preventing data loss, but replication only works with "live data". This means that replication ensures that you won't loose the data that a given index storees at the current point of time.
* Use snapshots for backups, and replication for high availability (and performance). Snapshots enable you to export the current state of the cluster or specific indeces to a file. This file can then be used to restore the state of the cluster or indices to that state. 
* So if we want to reindex the docs in a different way on prod, we can snapshot before to be able to recover.

## Second purpose of replication

It can be used to increase the throughput of a given index. Suppose we have a webshop where we hvee the prodex stored within a "products" index. We display the most popular products on the front page and we also run queries against the index when users search for products. This index gets queried a lot. The index has only one shard because we don't have many docs but we hve a lot of queries. 

We start experiencing a bottleneck in the search. The initial though can be to add an additional node to the cluster. Having one primary shard and one replica shard is not going to help because we cannot spread these out more then 2 nodes anyway. For us to utilize the additional node we would have to increase the number of shards or the # of replica shards. We don't want another node, so we can increase the # of replica shards by one or more. 

Since we have 2 nodes we are not increasing the avalability of the index but we **are increacing** the throughput of the index. 

**But how?**

Replica shard is a fully functional index on its own just like a shard is. This means that both of the replica shards can be queried at the same time. This is possible beccause of 2 things:

* ES routes requests to the best shard
* CPU paralelization improves performance if multiple replica shards are stored on the same node
* ES will automaticaly select the shard that will execute a given query, based on the # of factors. This means that if we have 3 queries at the same time they can be executed on the different shards

If the /health check returns "yellow", this means that probably we have one replica but it is not allocated in the node yet (it cannot be alocated in the same node).
