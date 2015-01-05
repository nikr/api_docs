Tags API
========
Use the Tags API explicitly to discriminate people by a tag given to them.  People tags are created implicitly by their use in the people API.

Index Endpoint
--------------
Show the tags that have been used before in a nation.

```
GET /api/v1/tags
```

### Parameters
* `limit` - max number of results to show in one page of results (default 10, max 100).
* `__nonce` - generated pagination nonce. Do not modify.
* `__token` - generated pagination token. Do not modify.

### Example

```
GET https://foobar.nationbuilder.com/api/v1/tags
```

```json
{
  "next": "/api/v1/tags?__nonce=3OUjEzI6iyybc1F3sk6YrQ&__token=ADGvBW9wM69kUiss1KqTIyVeQ5M6OwiL6ttexRFnHK9m",
  "prev": null,
  "results": [
    {
      "name": "doctor who"
    },
    {
      "name": "alien"
    },
    {
      "name": "human"
    }
  ]
}
```

People Endpoint
---------------
Search for people who have been tagged with the given tag.  Full representations will be returned.

```
GET /api/v1/tags/:tag/people
```

### Parameters
* `limit` - max number of results to show in one page of results (default 10, max 100).
* `__nonce` - generated pagination nonce. Do not modify.
* `__token` - generated pagination token. Do not modify.

### Example

To get the people who have been marked as 'doctor who', for example, you would issue this request:

```
GET https://foobar.nationbuilder.com/api/v1/tags/doctor%20who/people
```

And you will receive a response like this:

```json
{
  "next": "/api/v1/tags/doctor%20who/people?__nonce=3OUjEzI6iyybc1F3sk6YrQ&__token=ADGvBW9wM69kUiss1KqTIyVeQ5M6OwiL6ttexRFnHK9m",
  "prev": null,
  "results": [
    {
      "first_name": "Jack",
      "last_name": "Harkness",
      "email": "jack@torchwood.com",
      ...
    },
    {
      "first_name": "unknown",
      "last_name": "Who",
      "email": "thedoctor@tardis.com",
      ...
    }
  ]
}
```
