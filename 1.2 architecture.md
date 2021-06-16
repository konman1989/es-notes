## Node

An instance of ES that stores data. To ensure we can store teerrabytes of data we can set up as many nodes as we need to. Each node will store a part of our data. This way we can store data on multiple VM or physical machines which allows us to store terrabytes of data even if the machines disks has limits. A node refers to an instance of ES and not a machine, so you can run any number of nodes on the same machine. You can startup 5 nodes on your dev machine. You should separate things in prod so that each node runs on a dedicated machine, VM or within a container. 

Each node belongs to a cluster.

## Cluster

Collection of related nodes that together contain all of our data. We can have many clusters, but one is usually enough. Clusters are completely independent of each other by default. It's possible to perform cross-cluster searches but it is not very common to do so. You could run different clusters that server different puproses just to configure sings logically and configure things differently. 

When a node starts up it will either join an existing cluster if configured to do so, or it will create its own cluster consisting of just one node. ES node will always be a part of a cluster. 

## Document

Each unit of data that you store within a cluster is called a document. These are JSON objects containing whatever data you desire. When you index a document, the original JSON object that you sent to ES is stored along with some metadata that ES uses internally. Documents are just like a row in a relational database. Each document has a JSON format, a unique \_id  associated to it and pertains to a specific mapping/schema in the index. Documents are the things we search for. They can be more than text - any structured JSON data works. Every document has a unique \_id and a type.

{
  "name": "Bob",
  "country": "US"
}

-> ES

{
  "\_index": "people",
  "\_type": "doc",
  "\_id": "123",
  ...
  "\_source": {
    "name": "Bob",
    "country": "US"
  }
}

The documents are organized in indeces. Every document within ES is stored within and index. 

## Index

Groups documents together logically as well as provides configuration options that are related to scalability and availability. An index is a collection of docs that have similar characteristics and are logically related. 

It is similar to a table in a relational database which stores documents having a particular schema in JSON format. An index powers search into all documents within a collection of types. They contain inverted indices that let you search across everything within them at once. They may contain as many docs as you want. 

When we get to searching for data you will see that we specify the index that we want to search for docs, meaningg that search queries are actually run against indices. 


## Summary

* Nodes store the data the we add to ES (instance of ES)
* A cluster is a collection of nodes
* Data is stored as docs
* Docs are grouped together wih indices



