Subscription
=======

Endpoints:

- [Create subscription](#create-subscription)
- [Update subscription](#update-subscription)
- [Cancel subscription](#cancel-subscription)


Create Subscription
----------------------

* `POST /partners/subscriptions` will create an invite for the specific contact

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#token-param-authentication).

**Required parameters**:

* `pk` - the primary key of the user in your data store
* `email` - email address of the user (be sure to URL encode special
    characters)
* `plan` - the subscription plan for the account customer (`bark` or `bark_junior`)

Note: The `pk` is important to determine if the parent's account has already
been created and whether they have an existing parent account on Bark prior to
the referral.

The request body should be JSON-serialized with the following format:

```json
{
  "pk":    "MS2365",
  "email": "newuser@partner.com",
  "plan":  "bark"
}
```

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
  "error_type": "invalid_token"
}
```

`400 Bad Request`

```json
{
  "success":    false,
  "error":      "Partner PK has already been added",
  "error_type": "invalid_params"
}
```

```json
{
  "success":    false,
  "error":      "Email is blank",
  "error_type": "invalid_params"
}
```

Update Subscription
----------------------

* `PUT /partners/subscriptions/[pk]` will update the specified account in Bark

Note: The `pk` will be the one used to create the account.

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#token-param-authentication).

**Required parameters**:

* `plan` - the subscription plan for the account customer (`bark` or `bark_junior`)

The request body should be JSON-serialized with the following format:

```json
{
  "plan": "bark_junior"
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
  "error_type": "invalid_token"
}
```

`400 Bad Request`

```json
{
  "success":    false,
  "error":      "Please provide a valid pk",
  "error_type": "invalid_params"
}
```

`404 Not Found`

```json
{
  "success":    false,
  "error":      "Please provide a valid pk",
  "error_type": "invalid_params"
}
```

Cancel Subscription
----------------------

* `DELETE /partners/subscriptions` will delete the account Bark

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
