<details>
<summary>GET /user/:id/ban/</summary>
Get a paginated slice of user bans

|name|description|default|required|
| - | - | - | - |
|size|Number of items to fetch|50|False|
|offset|paginated index offset|0|False|

__responses__

- 200 - Bans
Bans cast on this user

```JSON
{
    "bans": [
        {
            "reason": "user given report reason",
            "user_id": "id of the user who created this ban",
            "id": "id of this ban",
            "created": "ban date",
            "expires": "ban expiry date"
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

- 403 - Forbidden
only admins may make this request

```JSON
{
    "error": "forbidden"
}
```


</details>
<details>
<summary>PUT /user/:id/ban/</summary>
Ban a user for some reason

__responses__

- 200 - User ban
A ban on a user

```JSON
{
    "ban": {
        "reason": "user given report reason",
        "user_id": "id of the user who created this ban",
        "id": "id of this ban",
        "created": "ban date",
        "expires": "ban expiry date"
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

- 403 - Forbidden
only admins may make this request

```JSON
{
    "error": "forbidden"
}
```


</details>


<details>
<summary>GET /user/:id/ban/:id/</summary>
Get information about a ban

__responses__

- 200 - User ban
A ban on a user

```JSON
{
    "ban": {
        "reason": "user given report reason",
        "user_id": "id of the user who created this ban",
        "id": "id of this ban",
        "created": "ban date",
        "expires": "ban expiry date"
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

- 403 - Forbidden
only admins may make this request

```JSON
{
    "error": "forbidden"
}
```

- 404 - No such ban for this user
A ban of this id does not exist for this user

```JSON
{
    "error": "no_such_ban"
}
```


</details>
<details>
<summary>DELETE /user/:id/ban/:id/</summary>
rescind a ban

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

- 403 - Forbidden
only admins may make this request

```JSON
{
    "error": "forbidden"
}
```

- 404 - No such ban for this user
A ban of this id does not exist for this user

```JSON
{
    "error": "no_such_ban"
}
```


</details>


<details>
<summary>GET /user/:id/reports/</summary>
Get a paginated slice of user reports

|name|description|default|required|
| - | - | - | - |
|size|Number of items to fetch|50|False|
|offset|paginated index offset|0|False|

__responses__

- 200 - Reports
Reports made on this resource

```JSON
{
    "reports": [
        {
            "reason": "user given report reason",
            "user_id": "id of the user who made this report",
            "id": "id of this report",
            "created": "report date"
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

- 403 - Forbidden
only admins may make this request

```JSON
{
    "error": "forbidden"
}
```


</details>
