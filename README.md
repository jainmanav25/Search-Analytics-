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
