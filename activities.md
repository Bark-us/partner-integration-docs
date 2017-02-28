Activities
=======

Endpoints:

- [Create an Activity](#create-an-activity)

Create an Activity
------

* `POST /activities` will create an activity in a child's connection in Bark

This endpoint requires [token header authentication](https://github.com/Bark-us/partner-integration-docs#authentication).

**Required parameters**:
* `activity` - the primary hash include to the activity's attributes

The following attributes are children of the `activity` has key:
* `connection_id` - the `connection_id` you would like the activity to be associated
* `posted_at` - the epoch integer in utc in seconds
* `message_id` - the primary key of the message as a string. duplicates aren't allowed.
* `message` - the text content of the message
* `author_name` - display friendly  name of the message author
* `author_id` - the primary id as a string of the message author
* `recipient_name` - display friendly name of the message recipient
* `recipient_id` - the primary id as a string of the message recipient
* `sent` - boolean sent status whether the message was sent by the bark child
* `provider` - string defining the platform (confirm with Bark engineering
    team)
* `type` - type of message as a string (eg. `chat`, `post`, `comment`, etc.)
* `media_url` - publicly accessible URL for media attachment

```json
{
    "activity": {
      "connection_id":  123,
      "posted_at":      1488320403,
      "message_id":     "8a5da52ed126447d359e70c05721a8aa",
      "message":        "Hey",
      "author_name":    "Bob",
      "author_id":      "1234",
      "recipient_name": "Jane",
      "recipient_id":   "5678",
      "sent":           true,
      "provider":       "acme",
      "type":           "chat",
      "media_url":      "http://example.com/image.png"
    }
}
```

##### Response

This endpoint will return `201 Created` if the activity was successfully
created.

If there's a problem with the payload, a `400 Bad Request` will be returned
along with a JSON response with `error` key with a value describing the error:

```json
{
  "error": "Please provide valid connection_id param"
}
```
or

```json
{
  "error": "Duplicate message_id"
}
```

If there's a problem with the authorization token, a `401 Unauthorized` will be returned
with the text `HTTP Token: Access denied.`
