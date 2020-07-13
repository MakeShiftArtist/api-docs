<details>
<summary>POST /auth/</summary>
Log in with an email/password, or an email/secret

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "email": "email of this account",
    "password": "password to this account",
    "secret": "or the secret produced by the server on last login"
}
```

__responses__

- 200 - Sucessful login
```JSON
{
    "auth": {
        "token": "Bearer token to be used in headers for authentication dependant requests",
        "expires": "expiry timestamp of this token",
        "secret": "secret to be used for logging in so that a password is not stored"
    }
}
```

- 400 - Bad Request
```JSON
{
    "error": "bad_request"
}
```

- 401 - Bad Auth
```JSON
{
    "error": "bad_auth"
}
```


</details>


<details>
<summary>GET /check/email/:email/</summary>
Check an email for availability

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Resource availability was checked
```JSON
{
    "exists": "does this resurce already exist bound to some user?"
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>GET /check/nick/:nick/</summary>
Check a nickname for availability

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Resource availability was checked
```JSON
{
    "exists": "does this resurce already exist bound to some user?"
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>POST /content/</summary>
Upload some image or video content. This should be a multipart POST with JSON data in part json, and the file upload in part file

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "mime": "content mime type",
    "nsfw": "is this content not safe for work?",
    "featurable": "may this content be featured?",
    "tags": [
        "list",
        "of",
        "tags"
    ]
}
```

__responses__

- 200 - Content was accepted
```JSON
{
    "content": {
        "id": "content id",
        "author": "authed user id",
        "tags": "content tags",
        "mime": "content mimetype",
        "like_count": "number of likes on this content",
        "dislike_count": "number of dislikes on this content",
        "repub_count": "number of repubs on this content",
        "view_count": "number of views on this content",
        "comment_count": "number of comments on this content",
        "created": "creation timestamp",
        "featured": "is this content featured?",
        "featurable": "may this content be featured?",
        "nsfw": "is this content nsfw?",
        "removed": "was this content removed?"
    }
}
```

- 400 - Bad Request
```JSON
{
    "error": "bad_request"
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 403 - Content was rejected
```JSON
{
    "error": "forbidden"
}
```

- 415 - Unsupported Media
```JSON
{
    "error": "bad_media"
}
```


</details>


<details>
<summary>GET /content/:id/</summary>
Get basic information about some content its id

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Content information
```JSON
{
    "content": {
        "id": "content id",
        "author": "author user id",
        "tags": "content tags",
        "mime": "content mimetype",
        "like_count": "number of likes on this content",
        "dislike_count": "number of dislikes on this content",
        "repub_count": "number of repubs on this content",
        "view_count": "number of views on this content",
        "comment_count": "number of comments on this content",
        "created": "creation timestamp",
        "featured": "is this content featured?",
        "featurable": "may this content be featured?",
        "nsfw": "is this content nsfw?",
        "removed": "was this content removed?"
    }
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such content
```JSON
{
    "error": "no_such_content"
}
```


</details>


<details>
<summary>GET /feed/all/</summary>
Get a paginated slice of the all feed

__query_strings__

|name|description|default|limit|required|
| - | - | - | - | - |
|size|Number of items to fetch|50|0 < it < 200|False|
|offset|paginated index offset|0|out of bounds indexes are not honored|False|

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Content feed
```JSON
{
    "content": [
        {
            "id": "content id",
            "author": "author user id",
            "tags": "content tags",
            "mime": "content mimetype",
            "like_count": "number of likes on this content",
            "dislike_count": "number of dislikes on this content",
            "repub_count": "number of repubs on this content",
            "view_count": "number of views on this content",
            "comment_count": "number of comments on this content",
            "created": "creation timestamp",
            "featured": "is this content featured?",
            "featurable": "may this content be featured?",
            "removed": "was this content removed?"
        },
        "..."
    ]
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>GET /me/</summary>
Get information about the authed user

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Self user information
```JSON
{
    "user": {
        "id": "your UUIDv4",
        "nick": "your nickname",
        "email": "your email",
        "bio": "bio (or, about) section",
        "subscriber_count": "number of users subscribed to this user",
        "subscription_count": "number of users this user has subscribed to",
        "post_count": "number of posts and reposts on this user's timeline",
        "created": "created time as a UNIX timestamp"
    }
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>POST /user/</summary>
Create a new user

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "email": "unused email to register",
    "nick": "unused nick to register",
    "password": "passowrd to bind to this account"
}
```

__responses__

- 200 - Account Created
```JSON
{
    "user": {
        "id": "user's UUIDv4",
        "nick": "user's nickname",
        "bio": "bio (or, about) section",
        "subscriber_count": "number of users subscribed to this user",
        "subscription_count": "number of users this user has subscribed to",
        "post_count": "number of posts and reposts on this user's timeline",
        "created": "unix creation timestamp"
    }
}
```

- 400 - Bad Request
```JSON
{
    "error": "bad_request"
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 403 - Forbidden
```JSON
{
    "error": "forbidden"
}
```

- 409 - Conflict
```JSON
{
    "conflict": "conflicting key"
}
```


</details>


<details>
<summary>GET /user/id/:id/</summary>
Get information about some user by their id

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - User information
```JSON
{
    "user": {
        "id": "user's UUIDv4",
        "nick": "user's nickname",
        "bio": "bio (or, about) section",
        "subscriber_count": "number of users subscribed to this user",
        "subscription_count": "number of users this user has subscribed to",
        "post_count": "number of posts and reposts on this user's timeline"
    }
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>PUT /user/id/:id/reports/</summary>
Report a usre for some reason

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "reason": "report reason"
}
```

__responses__

- 204 - Accepted
- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>GET /user/nick/:nick</summary>
Get information about some user by their nick

__request_headers__

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - User information
```JSON
{
    "user": {
        "id": "user's UUIDv4",
        "nick": "user's nickname",
        "bio": "bio (or, about) section",
        "subscriber_count": "number of users subscribed to this user",
        "subscription_count": "number of users this user has subscribed to",
        "post_count": "number of posts and reposts on this user's timeline"
    }
}
```

- 401 - Not Authorized
```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
```JSON
{
    "error": "no_such_user"
}
```


</details>
