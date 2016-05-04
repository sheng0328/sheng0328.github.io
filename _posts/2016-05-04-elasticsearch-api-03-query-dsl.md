---
title: Elasticsearch API 03 - Query DSL
header:
  teaser: elasticsearch.png
categories:
  - Elasticsearch
tags:
  - elasticsearch
---

## Introducing the Query Language

Elasticsearch provides a JSON-style domain-specific language that you can use to execute queries. This is referred to as the ```Query DSL```. The query language is quite comprehensive and can be intimidating at first glance but the best way to actually learn it is to start with a few basic examples.

If size is not specified, it defaults to 10:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match_all": {} },
  "size": 1
}
```

Return documents 11 through 20:

```js
 POST localhost:9200/bank/_search?pretty
 {
   "query": { "match_all": {} },
   "from": 10,
   "size": 10
 }
```

Sort results by account balance in descending order:

```js
 POST localhost:9200/bank/_search?pretty
 {
   "query": { "match_all": {} },
   "sort": { "balance": { "order": "desc" } }
 }
```
