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

Note: The `pk` is important to determine if the parent's account has already
been created and whether they have an existing parent account on Bark prior to
the referral.

**Optional parameters**:

* `child_birthday` - date of birthday as a string with format YYYY-MM-DD
* `child_name` - child's first name

If optional parameters are supplied, a child will automatically be added to the
account and the user will be immediately prompted to add connections for that
child.

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

