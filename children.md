Children
=======

Endpoints:

- [Create children](#create-children)
- [Delete children](#delete-children)

Create Children
------

* `POST /children` will create the requested children in Bark

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#authentication).

**Required parameters**:

* `token` - partner integration token we supply you

The request body should be JSON-serialized with the following format:

```json
{
    "children": [
      { "email": "billy@example.com", "domain": "example.com" },
      { "email": "johnny@example.com", "domain": "example.com" }
    ]
}
```

##### Response

If successfully created, the following JSON-serialized response will be
returned with a status of `201 Created`:


```json
{
  "success": true
}
```

If there is an error, an error with the following format will be returned:

`401 Unauthorized`

```json
{
  "success":    false,
  "error":      "Please provide a valid token",
  "error_type": "invalid_token",
}
```

`400 Bad Request`

```json
{
  "success":    false,
  "error":      "Please provide a valid list of children",
  "error_type": "invalid_params",
}
```

Delete Children
----------------------

* `DELETE /children` will delete the specified children in Bark

This endpoint requires [token authentication](https://github.com/Bark-us/partner-integration-docs#authentication).

**Required parameters**:

* `token` - partner integration token we supply you

The request body should be JSON-serialized with the following format:

```json
{
    "children": [
      { "email": "billy@example.com", "domain": "example.com" },
      { "email": "johnny@example.com", "domain": "example.com" }
    ]
}
```

If successfully created, the following JSON-serialized response will be
returned with a status of `200 OK`:


```json
{
  "success": true
}
```

If there is an error, an error with the following format will be returned:

`401 Unauthorized`

```json
{
  "success":    false,
  "error":      "Please provide a valid token",
  "error_type": "invalid_token",
}
```

`400 Bad Request`

```json
{
  "success":    false,
  "error":      "Please provide a valid list of children",
  "error_type": "invalid_params",
}
```
