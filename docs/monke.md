<details>
<summary>POST /auth/</summary>
Log in with an email/password, or an email/secret

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
Upload some image or video content

```JSON
{
    "mime": "content mime type",
    "nsfw": "is this content not safe for work?"
}
```

__responses__

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
<summary>POST /user/</summary>
Create a new user

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
The requested `nick` or `email` is already in use

```JSON
{
    "error": "<value>_conflict"
}
```


</details>


<details>
<summary>GET /user/:id/</summary>
Get information about some user by their id

__responses__

- 200 - User information
This user was found and their basic profile was returned

```JSON
{
    "id": "User's UUIDv4",
    "nick": "User's nickname",
    "bio": "bio (or, about) section",
    "subscriber_count": "number of users subscribed to this user",
    "subscription_count": "number of users this user has subscribed to",
    "post_count": "number of posts and reposts on this user's timeline",
    "created": "unix creation timestamp"
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
<summary>GET /user/nick/:nick</summary>
Get information about some user by their nick

__responses__

- 200 - User information
This user was found and their basic profile was returned

```JSON
{
    "id": "User's UUIDv4",
    "nick": "User's nickname",
    "bio": "bio (or, about) section",
    "subscriber_count": "number of users subscribed to this user",
    "subscription_count": "number of users this user has subscribed to",
    "post_count": "number of posts and reposts on this user's timeline",
    "created": "unix creation timestamp"
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
