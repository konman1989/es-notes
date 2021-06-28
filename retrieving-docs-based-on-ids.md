When we want to fetch a number of docs whose IDs you already know we can use this type of query. The case for it would be when we store the IDs of docs withing some kind of data store such as a relational DB, or if you want to use **the same identifiers in both places**.

```
GET /products/_search
{
  "query": {
    "ids": {
      "values": [1, 2, 3]
    }
  }
}
```

