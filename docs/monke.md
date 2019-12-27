<details>
<summary>POST /auth/</summary>
Log in with an email/password, or an email/secret

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
The information provided was correct a login token and new secret was produced

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
Request data is malformed or data is missing

```JSON
{
    "error": "bad_request"
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>GET /check/email/:email/</summary>
Check an email for availability

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Resource availability was checked
Information about the queried resource was returned

```JSON
{
    "exists": "does this resurce already exist bound to some user?"
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>GET /check/nick/:nick/</summary>
Check a nickname for availability

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Resource availability was checked
Information about the queried resource was returned

```JSON
{
    "exists": "does this resurce already exist bound to some user?"
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>POST /content/</summary>
Upload some image or video content. This should be a multipart POST with JSON data in part json, and the file upload in part file

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
The uploaded media was accepted and is being uploaded. Returned id may not yet be live

```JSON
{
    "content": {
        "id": "id of the created content"
    }
}
```

- 400 - Bad Request
Request data is malformed, data is missing, or the uploaded media does not match given mime

```JSON
{
    "error": "bad_request"
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 403 - Content was rejected
The uploaded content was rejected because this user is banned from content creation

```JSON
{
    "error": "forbidden"
}
```

- 415 - Unsupported Media
mimetype provided is not a supported upload type

```JSON
{
    "error": "bad_media"
}
```


</details>


<details>
<summary>GET /content/:id/</summary>
Get basic information about some content its id

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - Content information
This content was found and its basic information was returned

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
        "removed": "was this content removed?"
    }
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such content
Content of this id does not exist

```JSON
{
    "error": "no_such_content"
}
```


</details>


<details>
<summary>GET /feed/all/</summary>
Get a paginated slice of the all feed

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

|name|description|default|required|
| - | - | - | - |
|size|Number of items to fetch|50|False|
|offset|paginated index offset|0|False|

__responses__

- 200 - Content feed
A paginated slice of this feed

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
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```


</details>


<details>
<summary>POST /user/</summary>
Create a new user

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
This account was created

```JSON
{
    "user": "created"
}
```

- 400 - Bad Request
Request data is malformed or data is missing

```JSON
{
    "error": "bad_request"
}
```

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 403 - Forbidden
This device or ip address/range may not create users

```JSON
{
    "error": "forbidden"
}
```

- 409 - Conflict
The requested nick or email is already in use

```JSON
{
    "error": "<value>_conflict"
}
```


</details>


<details>
<summary>GET /user/:id/</summary>
Get information about some user by their id

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - User information
This user was found and their basic profile was returned

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

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
A user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>PUT /user/:id/reports/</summary>
Report a usre for some reason

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
The sent content was accepted and processed

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
A user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>GET /user/nick/:nick</summary>
Get information about some user by their nick

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 200 - User information
This user was found and their basic profile was returned

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

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such user
A user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```


</details>
