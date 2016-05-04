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

## Bool Query

The `bool` query allows us to compose smaller queries into bigger queries using boolean logic.

The occurrence types are:

* `must` - The clause (query) must appear in matching documents and will contribute to the score.
* `filter` - The clause (query) must appear in matching documents. However unlike must the score of the query will be ignored.
* `should`- The clause (query) should appear in the matching document. In a boolean query with no must or filter clauses, one or more should clauses must match a document. The minimum number of should clauses to match can be set using the minimum_should_match parameter.
* `must_not` - The clause (query) must not appear in the matching documents.

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
