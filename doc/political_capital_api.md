Political Capital API
==========

Resources
---------

### Capital Resource

* `id` - id of the Capital
* `person_id` - id of the person who received the Capital
* `author_id` - id of the person who created the Capital
* `type` - type of the Capital
* `amount_in_cents` - The amount of the Capital in cents.  Negative amount indicates deduction.
* `created_at` - timestamp representing when the Capital was created
* `content` - The reason for which the capital was awarded or deducted.

Index Endpoint
--------------

Use the index endpoint to get a paginated list of the Capitals of a person.

```
GET /api/v1/people/:id/capitals
```

### Parameters
* `limit` - max number of results to show in one page of results (default 10, max 100).
* `__nonce` - generated pagination nonce. Do not modify.
* `__token` - generated pagination token. Do not modify.

### Example

```
GET https://foobar.nationbuilder.com/api/v1/people/9/capitals
```

```json
{
  "next": "/api/v1/people/9/capitals?__nonce=3OUjEzI6iyybc1F3sk6YrQ&__token=ADGvBW9wM69kUiss1KqTIyVeQ5M6OwiL6ttexRFnHK9m",
  "prev": null,
  "results": [
    {
      "id": "3",
      "person_id": 9,
      "author_id": 4,
      "type": "Political Capital",
      "amount_in_cents": 500,
      "created_at": "2013-01-31T11:33:23-05:00",
      "content": {
          "note": "Award"
      }
    }
  ]
}
```

Create Endpoint
---------------

Creates a Capital for a person with the provided data.  Returns a full representation of the Capital which was created.  Returns errors if the creation fails.

```
POST /api/v1/people/:id/capitals
```

### Parameters

* `capital` - the resource of the Capital to be created

### Example

Make the request:

```
POST /api/v1/people/9/capitals
```

With attached body content like this:

```json
{
  "capital": {
    "amount_in_cents": 1550,
    "content": "Award"
  }
}
```
You will receive a response of status 200, with response body like this:

```json
{
  "capital": {
    "id": 7,
    "person_id": 9,
    "author_id": 12,
    "type": "Political Capital",
    "amount_in_cents": 1550,
    "created_at": "2013-01-31T11:33:23-05:00",
      "content": {
          "note": "Award"
      }
  }
}
```

Destroy Endpoint
----------------
Removes the Capital with the provided id from the person.  Takes no parameters, returns response code 204 on success.

```
DELETE /api/v1/people/:id/capitals/:id
```
