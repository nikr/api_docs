Precincts API
=============

Precinct Resource
-----------------
Precincts can be referenced by their id elsewhere in the API, for example in the
people API.

### Attributes
* `code` - Machine readable name of the precinct
* `name` - Human readable name of the precinct

Index Endpoint
--------------

Use the index endpoint to get a paginated list of the precincts in the nation.
This data can be used in the people API to attach a precinct to a person.

### Parameters
* `limit` - max number of results to show in one page of results (default 10, max 100).
* `__nonce` - generated pagination nonce. Do not modify.
* `__token` - generated pagination token. Do not modify.

```
GET /api/v1/precincts
```

### Example

```
GET https://foobar.nationbuilder.com/api/v1/precincts
```

```json
{
  "next": "/api/v1/precincts?__nonce=3OUjEzI6iyybc1F3sk6YrQ&__token=ADGvBW9wM69kUiss1KqTIyVeQ5M6OwiL6ttexRFnHK9m",
  "prev": null,
  "results": [
    {
      "id": 1,
      "code": "1337",
      "name": "test-precinct"
    },
    {
      "id": 2,
      "code": "0214",
      "name": "214 TUCKER CAPPS"
    },
    {
      "id": 3,
      "code": "0013",
      "name": "013 WILLIAMSON ROAD 4"
    },
    {
      "id": 4,
      "code": "0606",
      "name": "606 BEL AIR"
    },
    {
      "id": 5,
      "code": "0001",
      "name": "001 NORTH BEACH"
    },
    {
      "id": 6,
      "code": "0026",
      "name": "026 RALEIGH COURT 2"
    },
    {
      "id": 7,
      "code": "0011",
      "name": "011 WARD ELEVEN"
    },
    {
      "id": 8,
      "code": "0304",
      "name": "304 EAST IVY"
    },
    {
      "id": 9,
      "code": "0405",
      "name": "405 CALE"
    },
    {
      "id": 10,
      "code": "0512",
      "name": "512 YORK"
    }
  ]
}
```

Show Endpoint
-------------

Returns the information about an individual precinct with the given id.

```
GET /api/v1/precincts/:id
```

### Example

```
GET https://foobar.nationbuilder.com/api/v1/precincts/1
```

```json
{
  "precinct": {
    "id": 1,
    "code": "1337",
    "name": "test-precinct"
  }
}
```

Create Endpoint
---------------

Registers a precinct in the nation, to be referenced elsewhere.

```
POST /api/v1/precincts
```

### Example

Issuing this request:

```
POST https://foobar.nationbuilder.com/api/v1/precincts

{
  "precinct": {
    "code": "1338",
    "name": "test-precinct-2"
  }
}
```

Should create the precinct and return a response with code 200 and body like this:

```json
{
  "precinct": {
    "id": 498,
    "code": "1338",
    "name": "test-precinct-2"
  }
}
```

Update Endpoint
---------------

Use this endpoint to change the name and code of a precinct.  Note that partial
updates are not supported, you must do a full update of the record with code
and name.

```
PUT /api/v1/precincts/:id
```

### Example

Issuing this request:

```
PUT https://foobar.nationbuilder.com/api/v1/precincts/498

{
  "precinct": {
    "code": "1339",
    "name": "test-precinct-3"
  }
}
```

Should change the precinct to have those attributes, and return a response of
200 with the resource attached like this:

```json
{
  "precinct": {
    "id": 498,
    "code": "1339",
    "name": "test-precinct-3"
  }
}
```

Destroy Endpoint
----------------

Use this endpoint to remove the precinct from the system, and null out the
precinct field of the people who reside therein.

```
DELETE /api/v1/precincts/:id
```

### Example

To remove the precinct we have been manipulating, issue this request:

```
DELETE https://foobar.nationbuilder.com/api/v1/precincts/498
```

This should return an empty response with code 204, indicating successful
removal of the precinct.
