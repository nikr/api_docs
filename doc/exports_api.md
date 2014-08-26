Exports API
===========
This API allows you to create exports jobs to export lists from your nation.

Create/Run Endpoint
-------------------

Use this endpoint to export a list of people from your nation.
This will create and enqueue the export to run.

```
POST /api/v1/lists/:list_id/exports
```

### Query String

* `list_id` - The id of the list that you want to export

### Parameters

* `context` - "people" or "households".


Show Endpoint
-------------

Query export job status.

```
GET /api/v1/exports/:id
```

### Query String

* `id` - The id of the list that you want to export

### Example output

When a job is queued:

```json
{
  "export": {
    "id": 5,
    "type": "list",
    "context": "people",
    "status": {
      "name": "queued"
    },
    "download_url": null
  }
}
```

When a job is completed:

```json
{
  "export": {
    "id": 5,
    "type": "list",
    "context": "people",
    "status": {
      "name": "completed"
    },
    "download_url": 'http://s3.amazon.com/...'
  }
}
```

The `download_url` key contains the location of the exported file.


Delete Endpoint
---------------

Deletes an export when you no longer needs it.

```
DELETE /api/v1/exports/:id
```

### Parameters

* `id` - The export ID.

