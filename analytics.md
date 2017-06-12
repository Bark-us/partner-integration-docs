Analytics
=======

Endpoints:

- [Get Analytics](#get-analytics)

Get Analytics
------

* `GET /partners/analytics` will return analytics for a domain

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#token-param-authentication).

**Required parameters**:

* `token` - partner integration token we supply you
* `domain` - domain (`example.com`) of the school to get analytics

**Optional parameters**:

* `email` - email address of the child to get detail analytics

##### Response

If no `email` parameter is provided, the following JSON-serialized response will be
returned with a status of `200 Ok`:

```json
{
  "success": true,
  "children": {
    "unreviewed": [
      {
        "email": "jim@example.com",
        "total": 27
      },
      {
        "email": "sally@example.com",
        "total": 20
      },
      {
        "email": "bobby@example.com",
        "total": 7
      },
      {
        "email": "joe@example.com",
        "total": 2
      }
    ],
    "total": [
      {
        "email": "jim@example.com",
        "total": 104
      },
      {
        "email": "sally@example.com",
        "total": 84
      },
      {
        "email": "bobby@example.com",
        "total": 17
      }
    ],
  },
  "abuse_types": [
    {
      "name": "Cyberbullying",
      "total": 89
    },
    {
      "name": "Profanity / Swearing",
      "total": 63
    },
    {
      "name": "Inappropriate Behavior/Content",
      "total": 24
    },
    {
      "name": "3rd-Party-targeted Abusive Content",
      "total": 10
    }
  ]
}
```

_Note: Each category will return the top 10 of each type_

When an `email` is optionally provided as a query parameter, the analytics
response will be scoped to that child:

```json
{
  "success": true,
  "issues": {
    "total": 132,
    "reviewed": 89,
    "unreviewed": 43
  },
  "issues_review_url": "https://www.bark.us/snippets?t=1235",
  "abuse_types": [
    {
      "name": "Cyberbullying",
      "total": 89
    },
    {
      "name": "Profanity / Swearing",
      "total": 63
    },
    {
      "name": "Inappropriate Behavior/Content",
      "total": 24
    },
    {
      "name": "3rd-Party-targeted Abusive Content",
      "total": 10
    }
  ]
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
  "error":      "Unable to find a child with that email",
  "error_type": "invalid_params",
}
```

```json
{
  "success":    false,
  "error":      "Please provide a valid domain",
  "error_type": "invalid_params",
}
```