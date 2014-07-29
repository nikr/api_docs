# Memberships API

## Resources

### Membership resource

Name | Description | Writeable | Required | Examples
--- | --- | --- | --- | ---
name | The name of the membership | Y | Y | my_membership
person_id | The NationBuilder ID of the person the membership applies to | N | Y | 23
status | The current status of the membership, or a choice between "active", "grace period", "canceled", or "expired" | Y | N | active
status_reason | A description of how the membership acquired its current status | Y | N | prompt payment
expires_on | A timestamp representing when the membership expires | Y | N | 2014-07-21T13:48:51-07:00
started_at | A timestamp representing when the membership was started | Y | N | 2014-07-21T13:48:51-07:00
created_at | A timestamp representing when the membership was created | N | N | 2014-07-21T13:48:51-07:00
updated_at | A timestamp representing when the membership was last modified | N | N | 2014-07-21T13:48:51-07:00

## Index endpoint

This endpoint lists all memberships for a person.

```
GET /people/:person_id/memberships
```

### Parameters

* `person_id`
* `page` - the page to return
* `per_page` - the number of listing to display per page

### Example results

```json
{
    "page": 1,
    "total_pages": 1,
    "per_page": 10,
    "total": 1,
    "results": [
        {
            "name": "premier",
            "person_id": 2,
            "expires_on": null,
            "started_at": "2014-07-21T13:48:51-07:00",
            "created_at": "2014-07-21T13:48:51-07:00",
            "updated_at": "2014-07-21T13:48:51-07:00",
            "status": "active",
            "status_reason": null
        }
    ]
}
```

## Create endpoint

This endpoint creates a membership for a person.

```
POST /people/:person_id/memberships
```

### Parameters

* `person_id`
* `membership` - JSON corresponding to the parameters of the new membership

### Example results

POSTing to:

```
/people/:person_id/memberships
```

with this JSON body:

```json
{
    "membership":  {
        "name": "my membership",
        "status": "active",
        "status_reason": "paid",
        "started_at": "2014-07-28T15:30:48-07:00",
        "expires_on": "2014-09-28T15:30:48-07:00"
    }
}
```

results in:

```json
{
    "membership": {
        "name": "my membership",
        "person_id": 2,
        "expires_on": "2014-09-28T15:30:48-07:00",
        "started_at": "2014-07-28T15:30:48-07:00",
        "created_at": "2014-07-28T15:31:50-07:00",
        "updated_at": "2014-07-28T15:31:50-07:00",
        "status": "active",
        "status_reason": "paid"
    }
}
```

## Update endpoint

This endpoint updates a membership for a person.

```
PUT /people/:person_id/memberships
```

### Parameters

* `person_id`
* `membership` - JSON corresponding to the parameters of the new membership. The `name` parameter must be provided.

### Example results

PUTing to:

```
/people/:person_id/memberships
```

with this JSON body:

```json
{
    "membership":  {
        "name": "my membership",
        "status": "expired",
        "status_reason": "did not pay bill"
    }
}
```

results in:

```json
{
    "membership": {
        "name": "my membership",
        "person_id": 2,
        "expires_on": "2014-07-28T00:00:00+00:00",
        "started_at": "2014-07-28T15:30:48-07:00",
        "created_at": "2014-07-28T15:31:50-07:00",
        "updated_at": "2014-07-28T15:37:40-07:00",
        "status": "expired",
        "status_reason": "did not pay bill"
    }
}
```

## Destroy endpoint

This endpoint destroys a membership.

```
DELETE /people/:person_id/memberships/:membership_name
```

### Parameters

* `person_id`
* `membership_name` - the name of the membership to destroy

### Example usage

```
DELETE /people/:person_id/memberships/:membership_name
```
