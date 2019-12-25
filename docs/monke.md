<details>
<summary>POST /user/</summary>
Create a new user

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "email": "<account_email>",
    "nick": "<account_nick>",
    "password": "<account_password>"
}
```

__responses__

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 400 - Bad Request
Request data is malformed or data is missing

```JSON
{
    "error": "bad_request"
}
```

- 200 - Account Created
This account was created

```JSON
{
    "user": "created"
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
<summary>GET /user/:id</summary>
Get information about some user by their id

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

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

- 404 - No such user
A user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>GET /users/nick/:nick</summary>
Get information about some user by their nick

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

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

- 404 - No such user
A user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```


</details>


<details>
<summary>POST /auth/</summary>
Log in with an email/password, or an email/secret

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

```JSON
{
    "email": "<account_email>",
    "password": "<account_password>",
    "secret": "or the secret produced by the server on last login"
}
```

__responses__

- 401 - Not Authorized
No Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 400 - Bad Request
Request data is malformed or data is missing

```JSON
{
    "error": "bad_request"
}
```

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


</details>
