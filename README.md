The Bark.us Partner Integration
==============================

![Bark Logo](https://www.bark.us/bark-logo-sm.png)

Welcome to the Bark.us Partner Integration documentation. Looking to
integration your existing product with Bark? You've come to the right place!

Making a request
----------------

All URLs start with `https://www.bark.us/api/v1/parnters`. **HTTPS only**.
If we change the API in backward-incompatible ways, we'll bump the version
marker and maintain stable support for the old URLs.

Authentication
--------------

As part of your integration, you'll be given a `token` and `secret`. The token
will be included as a query string parameter, while the `secret` will be used
to sign the request.

_Note: Your `secret` should be kept secure at all times.
Do not share this Secret with anyone, do not include it in JavaScript code or a mobile client.
We're happy to reset your `secret` to a new value at any time, if you
suspect that it was leaked._

Request Signing
---------------

```
string to sign: endpoint|key1=value1|key2=value2|...

Parameter name: signature
Parameter value: signed token with your Secret using the SHA256 hash algorithm
```

string to sign: API endpoint appended with a concatenation of all key/value pairs of your
request parameters, sorted by key in ascending order.
Each key/value pair is separated by the pipe character.

The signature describes the hex representation of a RFC 2104-compliant HMAC with
the SHA256 hash algorithm, using the API endpoint, your request parameters and
your `secret`. Most programming languages provide the tools to create
such a signature. Here are some examples to get you started.

#### Python

```python
# -*- coding: UTF-8 -*-
import hmac
from hashlib import sha256

def generate_signature(endpoint, params, secret):
    sig = endpoint
    for key in sorted(params.keys()):
        sig += '|%s=%s' % (key, params[key])
    return hmac.new(secret, sig, sha256).hexdigest()
```

#### Ruby

```ruby
require 'openssl'
require 'base64'

def generate_signature(endpoint, params, secret)
  string_to_sign = endpoint

  Hash[params.sort_by { |k, v| k }].each do |k, v|
    string_to_sign += "|%s=%s" % [k, v]
  end

  digest = OpenSSL::Digest::Digest.new('sha256')
  OpenSSL::HMAC.hexdigest(digest, secret, string_to_sign)
end
```

#### PHP

```php
<?php
function generate_signature($endpoint, $params, $secret) {
  $sig = $endpoint;
  ksort($params);
  foreach ($params as $key => $val) {
    $sig .= "|$key=$val";
  }
  return hash_hmac('sha256', $sig, $secret, false);
}
```

### Request Example

Partner Token: `XdJihWNXYbaLzK4n`
Partner Secret: `M6Atnz1rEAARBJ8G`

Endpoint: `/signup`

Parameters:
- pk: `a4afed11-06cb-4f59-9522-82932e16c5d5`
- email: `me@example.com`
- token: `XdJihWNXYbaLzK4n`

With the endpoint and parameters above, the signature would be:

`signature` : `6f469b342bf6dca4213ab3093d885199ded0d7eca162823c5c2e76487eb38931`

The final request with the params above would be:

`GET`
`https://www.bark.us/api/v1/partners/signup?pk=a4afed11-06cb-4f59-9522-82932e16c5d5&email=me%40example.com&token=XdJihWNXYbaLzK4n&signature=6f469b342bf6dca4213ab3093d885199ded0d7eca162823c5c2e76487eb38931`

_Note: The `email` parameter needs to be encoded in the request URL.
The email address should **NOT** be encoded when generating the signature._

API endpoints
-------------
- [Signup](https://github.com/Bark-us/partner-integration-docs/blob/master/signup.md)

Support
-------

If you have a specific feature request or if you found a bug, [please open a GitHub issue](https://github.com/Bark-us/partner-integration-docs/issues). We encourage forking these docs for local reference, and will happily accept pull request with agreed improvements.

Alternatively, you can reach us via email at <help@bark.us>.
