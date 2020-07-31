Subscription
=======

Endpoints:

- [Cancel subscription](#cancel-subscription)


Cancel Subscription
----------------------

* `DELETE /partners/subscriptions` will delete the specified children in Bark

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#token-param-authentication).

**Required parameters**:

* `pk` - the primary key of the user in your data store

Note: The `pk` is important to determine if the parent's account has already
been created and whether they have an existing parent account on Bark prior to
the referral.

The request body should be JSON-serialized with the following format:

```json
{
  "pk": "MS2365"
},
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
  "error":      "Please provide a valid pk",
  "error_type": "invalid_params",
}
```

`404 Not Found`

```json
{
  "success":    false,
  "error":      "Please provide a valid pk",
  "error_type": "invalid_params",
}
```
