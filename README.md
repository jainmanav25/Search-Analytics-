# Elasticsearch: Search Slow Logs

## Step 1: Put Sample Data in an Index

```json
PUT slow-logs-test
{
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "description": { "type": "text" },
      "author": { "type": "keyword" },
      "publish_date": { "type": "date" },
      "views": { "type": "integer" },
      "tags": { "type": "keyword" }
    }
  }
}

POST slow-logs-test/_doc/1
{
  "title": "Learning Elasticsearch",
  "description": "A comprehensive guide to Elasticsearch",
  "author": "John Doe",
  "publish_date": "2023-01-01",
  "views": 1500,
  "tags": ["elasticsearch", "search", "guide"]
}

POST slow-logs-test/_doc/2
{
  "title": "Advanced Search Techniques",
  "description": "Mastering advanced search capabilities in Elasticsearch",
  "author": "Jane Smith",
  "publish_date": "2022-05-15",
  "views": 2500,
  "tags": ["elasticsearch", "search", "advanced"]
}

POST slow-logs-test/_doc/3
{
  "title": "Scaling Elasticsearch",
  "description": "Learn how to scale your Elasticsearch cluster efficiently",
  "author": "Alice Johnson",
  "publish_date": "2021-12-20",
  "views": 3500,
  "tags": ["elasticsearch", "scaling", "performance"]
}

POST slow-logs-test/_doc/4
{
  "title": "Elasticsearch Query DSL",
  "description": "A deep dive into Elasticsearch's Query DSL",
  "author": "Bob Brown",
  "publish_date": "2020-11-11",
  "views": 1200,
  "tags": ["elasticsearch", "query", "dsl"]
}

POST slow-logs-test/_doc/5
{
  "title": "Optimizing Elasticsearch",
  "description": "Tips and tricks for optimizing Elasticsearch performance",
  "author": "Emma Wilson",
  "publish_date": "2019-10-05",
  "views": 1800,
  "tags": ["elasticsearch", "optimization", "performance"]
}

```
## Step 2: Make Index Pattern Named elastic-cloud-logs*

## Step 3: Change the Search Slow Logs Settings

```json
PUT /slow-logs-test/_settings
{
  "index.search.slowlog.threshold.query.warn": "10s",
  "index.search.slowlog.threshold.query.info": "5s",
  "index.search.slowlog.threshold.query.debug": "2s",
  "index.search.slowlog.threshold.query.trace": "500ms",
  "index.search.slowlog.threshold.fetch.warn": "1s",
  "index.search.slowlog.threshold.fetch.info": "800ms",
  "index.search.slowlog.threshold.fetch.debug": "500ms",
  "index.search.slowlog.threshold.fetch.trace": "200ms"
}
```
## Step 4: Apply Search Queries to Check Slow Logs Settings
```json
GET slow-logs-test/_search
{
  "query": {
    "match_all": {}
  }
}

GET slow-logs-test/_search
{
  "query": {
    "match": {
      "description": "guide"
    }
  }
}

GET slow-logs-test/_search
{
  "query": {
    "term": {
      "author": {
        "value": "Jane Smith"
      }
    }
  }
}

```
## Step 5: Add Search Field Names
Make sure to add the following search fields:

```bash
elasticsearch.slowlog.source
elasticsearch.slowlog.took
```
## Conclusion
This document provides a step-by-step guide to configuring and checking the Search Slow Logs settings in Elasticsearch. The steps outlined above allow you to put sample data in an index, modify slow log settings, apply search queries, and verify slow log results.


