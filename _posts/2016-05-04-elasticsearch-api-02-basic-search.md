---
title: Elasticsearch API 02 - Basic Search
header:
  teaser: elasticsearch.png
categories:
  - Elasticsearch
tags:
  - elasticsearch
---

## Loading Sample Dataset
Download sample dataset [here](https://github.com/bly2k/files/blob/master/accounts.zip?raw=true). Extract file and load it as follows:

```js
POST localhost:9200/bank/account/_bulk?pretty
```

Paste sample dataset at request body as follows:

```js
{"index":{"_id":"1"}}
{"account_number":1,"balance":39225,"firstname":"Amber","lastname":"Duke","age":32,"gender":"M","address":"880 Holmes Lane","employer":"Pyrami","email":"amberduke@pyrami.com","city":"Brogan","state":"IL"}
{"index":{"_id":"6"}}
{"account_number":6,"balance":5686,"firstname":"Hattie","lastname":"Bond","age":36,"gender":"M","address":"671 Bristol Street","employer":"Netagy","email":"hattiebond@netagy.com","city":"Dante","state":"TN"}
...
```

Check indices:

```json
GET localhost:9200/_cat/indices?v

health index pri rep docs.count docs.deleted store.size pri.store.size
yellow bank    5   1       1000            0    424.4kb        424.4kb
```

## The Search API
There are two basic ways to run searches: one is by sending search parameters through the ```REST request URI``` and the other by sending them through the ```REST request body```.

Search request:

```js
GET localhost:9200/bank/_search?q=*&pretty
{
  "took" : 63,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1000,
    "max_score" : 1.0,
    "hits" : [ {
      "_index" : "bank",
      "_type" : "account",
      "_id" : "1",
      "_score" : 1.0, "_source" : {"account_number":1,"balance":39225,"firstname":"Amber","lastname":"Duke","age":32,"gender":"M","address":"880 Holmes Lane","employer":"Pyrami","email":"amberduke@pyrami.com","city":"Brogan","state":"IL"}
    }, {
      "_index" : "bank",
      "_type" : "account",
      "_id" : "6",
      "_score" : 1.0, "_source" : {"account_number":6,"balance":5686,"firstname":"Hattie","lastname":"Bond","age":36,"gender":"M","address":"671 Bristol Street","employer":"Netagy","email":"hattiebond@netagy.com","city":"Dante","state":"TN"}
    }, {
      "_index" : "bank",
      "_type" : "account",
```

Using Query DSL:

```js
POST localhost:9200/bank/_search?pretty
{
  "query": { "match_all": {} }
}
```
