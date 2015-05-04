Page Attachments API
====================

Index Endpoint
--------------
The index endpoint lists a page's file attachments

```
GET /api/v1/sites/:site_slug/pages/:page_slug/attachments
```

### Parameters
* `limit` - max number of results to show in one page of results (default 10, max 100).
* `__nonce` - generated pagination nonce. Do not modify.
* `__token` - generated pagination token. Do not modify.

### Example

```
GET https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/blog/attachments
```

```json
{
  "next": null,
  "prev": null,
  "results": [
    {
      "id": 6,
      "filename": "Green_Apple.gif",
      "updated_at": "2013-06-04T14:16:14-07:00",
      "content_type": "image/gif",
      "url": "http://d3n8a8pro7vhmx.cloudfront.net/foobar/pages/20/attachments/original/1370380574/Green_Apple.gif?1370380574"
    },
    {
      "id": 7,
      "filename": "RedDog.gif",
      "updated_at": "2013-06-06T10:15:02-07:00",
      "content_type": "image/gif",
      "url": "http://d3n8a8pro7vhmx.cloudfront.net/foobar/pages/20/attachments/original/1370538902/RedDog.gif?1370538902"
    }
  ]
}
```

Create Endpoint
---------------
The create endpoint attaches a file to a page

```
POST /api/v1/sites/:site_slug/pages/:page_slug/attachments
```

### Parameters

* attachment - parameters for the new page attachment
    * filename - name for the provided file
    * content_type - MIME type string for the provided file
    * updated_at - when the file was last updated
    * content - Base 64 encoded representation of the file, with standard RFC 4648

The response will not contain the file content, but all representations of this resource will include a url at which you can host the file.

### Example

Issuing this request:

```
POST https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/pool_event/attachments
```

With this attached body:

```json
{
  "attachment": {
    "filename": "file.jpg",
    "content_type": "image/jpeg",
    "updated_at": "2013-06-06T10:15:02-07:00",
    "content": "/9j/4AAQSkZJRgABAQEBjwGPAAD//gBTRmlsZSBzb3VyY2U6IGh0d..."
  }
}
```

Should create the attachment and respond with status code 200, and a body like this:

```json
{
  "attachment": {
    "filename": "file.jpg",
    "content_type": "image/jpeg",
    "updated_at": "2013-06-06T10:15:02-07:00",
    "url": "http://d3n8a8pro7vhmx.cloudfront.net/foobar/pages/20/attachments/original/1370538902/file.jpg?1370538902"
  }
}
```

Show Endpoint
-------------
The read endpoint returns the metadata for a single page attachment

```
GET /api/v1/sites/:site_slug/pages/:page_slug/attachments/:id
```

### Example

Issuing this request:

```
GET https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/pool_event/attachments/:id
```

Should get you a 200 status code response like this:

```json
{
  "attachment": {
    "filename": "file.jpg",
    "content_type": "image/jpeg",
    "updated_at": "2013-06-06T10:15:02-07:00",
    "url": "http://d3n8a8pro7vhmx.cloudfront.net/foobar/pages/20/attachments/original/1370538902/file.jpg?1370538902"
  }
}
```

Destroy Endpoint
----------------
Removes an attachment from a page.  Returns status code 204 to denote success.

```
DELETE /api/v1/sites/:site_slug/pages/:page_slug/attachments/:id
```
