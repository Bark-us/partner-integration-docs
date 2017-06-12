Signup
=======

Endpoints:

- [Signup](#signup)

Signup
------

* `GET /partners/signup` will create the requested user in Bark

This endpoint requires [token param authentication](https://github.com/Bark-us/partner-integration-docs#token-param-authentication).

**Required parameters**:

* `pk` - the primary key of the user in your data store
* `email` - email address of the user
* `token` - partner integration token we supply you

##### Response

This endpoint will return redirect the user to the
appropriate page inside Bark upon signup.

`email` param should be properly URL encoded to retain any special characters
not safely sent through a URL.

Note: This endpoint can safely be used multiple times for a parent. If the
parent has already signed up, it will not create another, but rather forward
them safely in to the site while authenticating them as their original Bark
account.

If there is an error, an error with the following format will be returned:

`401 Unauthorized`

```json
{
  "success":    false,
  "error":      "Please provide a valid token",
  "error_type": "invalid_token",
}
```

