The Bark.us Partner Integration
==============================

![Bark Logo](https://www.bark.us/bark-logo-sm.png)

Welcome to the Bark.us Partner Integration documentation. Looking to
integration your existing product with Bark? You've come to the right place!

How does it work?
-----------------

Within a product/service that wants to offer Bark's services to their customers, this
integration offers the partner the ability to set up single buttons/links to allow their users
the ability to sign up for Bark with 1 click, and associates the signup to their company. After clicking this link in the partner's site/app, the user can then configure Bark-specific details (e.g. connecting social media accounts, text messaging, emails, etc.).

For example, during registration within your product/service, you might offer a
checkbox or link offering Bark registration and the benefits.

The [Signup API](https://github.com/Bark-us/partner-integration-docs/blob/master/signup.md)
are configured such that they can also be used
even if the user is already registered on Bark. If that's the case, the
user will be authenticated as their existing account and redirected to their
Bark dashboard, allowing you to use it the same link within your
product/service's dashboard or profile.

Making a request
----------------

All URLs start with `https://www.bark.us/api/v1/`. **HTTPS only**.
If we change the API in backward-incompatible ways, we'll bump the version
marker and maintain stable support for the old URLs.

Authentication
--------------

Each endpoint will designate which means of authentication is required.

### Token Header Authentication

The first requires an access token (we'll refer to this as "token
header authentication") for which you supply in the `Authorization` header:

If you're token is `1234567890`, you'd add the following header:

`Authorization: Token token=1234567890`

### Token Param Authentication

The second requires an access token (we'll refer to this as "token
param authentication") for which you can supply in 2 ways when
communicating with the API:

1. Provide the `X-Token-Auth` header with the value being your integration token
2. Include the query string param `token` (ie. `https://www.bark.us/api/v1/partners/children?token=mysecrettoken`)

API endpoints
-------------
- [Signup](https://github.com/Bark-us/partner-integration-docs/blob/master/signup.md)
- [Children](https://github.com/Bark-us/partner-integration-docs/blob/master/children.md)
- [Activities](https://github.com/Bark-us/partner-integration-docs/blob/master/activities.md)
- [Analytics](https://github.com/Bark-us/partner-integration-docs/blob/master/analytics.md)

Support
-------

If you have a specific feature request or if you found a bug, [please open a GitHub issue](https://github.com/Bark-us/partner-integration-docs/issues). We encourage forking these docs for local reference, and will happily accept pull request with agreed improvements.

Alternatively, you can reach us via email at <help@bark.us>.
