---
title: Elasticsearch API 04 - Executing Searches
header:
  teaser: elasticsearch.png
categories:
  - Elasticsearch
tags:
  - elasticsearch
---

## Executing Searches

This example shows how to return two fields, account_number and balance (inside of `_source`), from the search:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match_all": {} },
  "_source": ["account_number", "balance"]
}
```

This example returns the account numbered 20:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match": { "account_number": 20 } }
}
```

This example returns all accounts containing the term "mill" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match": { "address": "mill" } }
}
```

This example returns all accounts containing the term "mill" or "lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match": { "address": "mill lane" } }
}
```

This example is a variant of match (match_phrase) that returns all accounts containing the phrase "mill lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match_phrase": { "address": "mill lane" } }
}
```

This example composes two match queries and returns all accounts containing "mill" and "lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": {
    "bool": {
      "must": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```

In contrast, this example composes two match queries and returns all accounts containing "mill" or "lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": {
    "bool": {
      "should": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```

This example composes two match queries and returns all accounts that contain neither "mill" nor "lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": {
    "bool": {
      "must_not": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```

This example composes two match queries and returns all accounts that contain neither "mill" nor "lane" in the address:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
  }
}
```
