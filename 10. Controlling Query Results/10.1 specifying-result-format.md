## Return YAML instead of JSON

```
GET /recepies/_search?format=yaml
{
  "query": {
    "match": {
      "title": "pasta"
    }
  }
}
```

The returned response is in the YAML format

We get prettified JSON result in Kibana, but for curl queries it is not formatted by default. 

```
GET /recepies/_search?pretty
{
  "query": {
    "match": {
      "title": "pasta"
    }
  }
}
```

