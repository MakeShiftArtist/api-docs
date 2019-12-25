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

- 401 - Not AuthorizedNo Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - Not FoundThis route was not found, or the information of this dynamic route is not found

```JSON
{
    "error": "not_found"
}
```

- 400 - Bad RequestRequest data is malformed or data is missing

```JSON
{
    "error": "bad_request"
}
```

- 200 - Account CreatedThis account was created

```JSON
{
    "user": "created"
}
```

- 403 - ForbiddenThis device or ip address/range may not create users

```JSON
{
    "error": "forbidden"
}
```

- 409 - ConflictThe requested `nick` or `email` is already in use

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

- 401 - Not AuthorizedNo Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such userA user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```

- 200 - User informationThis user was found and their basic profile was returned

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


</details>


<details>
<summary>GET /users/nick/:nick</summary>
Get information about some user by their nick

|name|value|required|
| - | - | - |
|Authorization|Basic or Bearer authorization|True|

__responses__

- 401 - Not AuthorizedNo Authorization header was included with this request

```JSON
{
    "error": "not_authorized"
}
```

- 404 - No such userA user of this id does not exist

```JSON
{
    "error": "no_such_user"
}
```

- 200 - User informationThis user was found and their basic profile was returned

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


</details>
