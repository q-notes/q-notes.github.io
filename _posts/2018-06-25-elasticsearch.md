---
layout: post
title:  "elasticsearch"
date:   2018-06-25 19:38:00 +0700
categories: elasticsearch
---
+ delete index
```sh
$ curl -XDELETE 'localhost:9200/twitter?pretty'
```

+ check if index exists
```sh
$ curl -XHEAD 'localhost:9200/twitter?pretty'
```

+ copy index
```sh
$ curl -XPOST 'localhost:9200/_reindex?pretty' \
       -H 'Content-Type: application/json' \
       -d'
{
  "source": {
    "index": "tw"
  },
  "dest": {
    "index": "twitter"
  },
  "script": {
    "inline": "ctx._id = ctx._source.id"
  }
}'
```

+ update [refresh_interval](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-update-settings.html#bulk)
```sh
$ curl -XPUT 'localhost:9200/twitter/_settings?pretty' \
       -H 'Content-Type: application/json' \
       -d'
{
    "index" : {
        "refresh_interval" : "60s"
    }
}'
```

+ copy_to: title, content -> text fields
```sh
$ curl -XPUT 'localhost:9200/web?pretty' \
       -H 'Content-Type: application/json' \
       -d'
{
  "mappings": {
    "docs": {
      "properties": {
        "title": {
          "type": "text",
          "copy_to": "text" 
        },
        "content": {
          "type": "text",
          "copy_to": "text" 
        },
        "text": {
          "type": "text"
        }
      }
    }
  }
}'
```

+ [specific date fields](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-date-format.html)
```sh
$ curl -XPUT 'localhost:9200/web?pretty' \
       -H 'Content-Type: application/json' \
       -d '
{
  "mappings": {
    "docs": {
      "properties": {
        "creationDate": {
          "type":   "date"
        },
        "captureDate": {
          "type":   "date"
        }
      }
    }
  }
}'
```
