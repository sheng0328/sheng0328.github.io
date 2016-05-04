---
title: Elasticsearch API 04 - Executing Filters
header:
  teaser: elasticsearch.png
categories:
  - Elasticsearch
tags:
  - elasticsearch
---

## Executing Filters

* The `bool` query also supports filter clauses which allow to use a query to restrict the documents that will be matched by other clauses, without changing how scores are computed.
* The `range` query, which allows us to filter documents by a range of values. This is generally used for numeric or date filtering.

This example uses a bool query to return all accounts with balances between 20000 and 30000, inclusive. In other words, we want to find accounts with a balance that is greater than or equal to 20000 and less than or equal to 30000.

```js
POST localhost:9200/bank/_search?pretty
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}```
