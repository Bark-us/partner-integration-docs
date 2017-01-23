Signup
=======

Endpoints:

- [Signup](#signup)
- [Signup Signature Check](#signup-signature-check)

Signup
------

* `GET /signup` will create the requested user in Bark

**Required parameters**:

* `pk` - the primary key of the user in your data store
* `email` - email address of the user
* `token` - partner integration token we supply you
* `signature` - HMAC signature of request parameters (endpoint for signature
    generation is `/signup`)

##### Response

This endpoint will return redirect the user to the
appropriate page inside Bark upon signup.

Signup Signature Check
----------------------

* `GET /signup/check` will check supplied signature for accuracy. During
    development, it's worth using this endpoint to ensure you're appropriately
    generating signatures.

**Required parameters**:

* `pk` - the primary key of the user in your data store
* `email` - email address of the user
* `token` - partner integration token we supply you
* `signature` - HMAC signature of request parameters (endpoint for signature
    generation is `/signup/check`)

##### Response

This endpoint will return `200 Success` with the text `Signature is valid` if
signature matches.

If the signature is not valid, you might receive one of the following
responses:

- `400 Bad Request` - if `email`, `pk`, `signature` parameter is missing, or
    `signature` isn't accurate
- `401 Unauthenticated` - if the `token` parameter is missing or isn't correct

In addition to these responses, an error message will be returned in plain
text indicating the reason for failure.

