## Sharding

Is a way to divide an index into separate pieces where each piece is called a shard. Sharding is done at the index level. Each document is hashed to a shard so we can quickly figure out which shard owns a given document. As a user of Elasticsearch, we only need to specify the number of primary and replica shards for an index and should never deal with shards individually but only at the index level. Elasticsearch distributes shards amongst all nodes in the cluster and can move shards automatically from one node to another in the case of a node failure, or the addition of new nodes.

The main reason for dividing an index into multiple shards is to be able to horizontally scale the data volume. Each node can contain many shards.

### Example

We have 2 nodes with a capacity of 500 GB for each and an index of 600 GB that won't fit in any of them. Since a shard mmust be placed within a single node, we can divide the index into 2 shards 300 GB each. 

* A shard is an independent index ... kind of
* Each shard is an Apache Lucene index
* An ES index consists of one or more Lucene indices
* A shard may store up to about 2 BLN docs.
* The main reason for sharding an index is to be able to scale its data volume, being the number of documents it can store. By using sharding, you can store billions of documents within and index.
* To easier fit large indices into smaller chunks to fit nodes
* It enables queries to be distributed and parallelized across an index' shards. It means that a search query can be run on multiple shards at the same time.


### How many shards are optimal?

* There is no formula for that
* There are many factors involved
* Factors include # of the nodes and their capacity, # of indices and their sizes, # of queries etc.

However, as a **rule of thumb**, a decent place to start would be to choose five shards if you anticipate millions of documents to be added to an index. If these are only thousands, stick to default settings and increase if needed.

## Summary

* Sharding splits indeces to smaller pieses
* Increases the # of docs an index can store
* Makes it easier to fit large indices onto nodes
* May improve query throughput
* Index defaults to having one shard
* Add a couple of shard for large indeces
