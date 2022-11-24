# API documentation

### Create user

| Parameter | Required | Allowed values |
| --------- | -------- | ------- |
| email    | **Yes**      | Valid email address       |
| gender | **Yes** | `0` - male, `1` - female
| age | **Yes** | `18` - `100` |
| username | **Yes** | Between 3 and 15 characters. Numbers (max 4 digits), letters, dash and underscore are allowed. |
| ethnicity | No | `0` - white,`1` - black, `2` - asian, `3` - hispanic, `4` - indian, `5` - eastern `6` - other |
| lang | No | `en` - English, `it` - Italian, `de` - German, `fr` - French

Example request:

```shell
curl --location --request POST 'https://members.4sd.com/api/affiliate/user' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{your_api_key}}' \
--data-raw '{
    "username": "JohnDoe",
    "email": "johndoe@mail.com",
    "age": 25,
    "gender": 0,
    "lang": "en"
}'
```

If the request is accepted, you will get `200` status code with the link in the response payload:
After redirecting user to the received **redirect** link, user will be logged in automatically.
```json
{
    "redirect": "https://members.4sd.com/search?auto=https%3A%2F%sugardaddy.date%3Awithsomeparameters"
}
```

### Affiliate data

You can pull information about your account, you should send the GET request like the one below:
```shell
curl --location --request GET 'https://members.4sd.com/api/affiliate' \
--header 'x-api-key: {{your_api_key}}'
```

Example response:
```json
{
    "name": "Test affiliate",
    "active": 1,
    "users_registered": 3,
    "initial_payments": 2,
    "repeated_payments": 3,
    "created_at": "2021-11-02 11:35:16"
}
```

### Listing registered users
You are able to list all users that have been registered with your api_key

Example request:

```
curl --location --request GET 'https://members.4sd.com/api/affiliate/user?page=1' \
--header 'x-api-key: {{your_api_key}}'
```

Example response:

```json
{
    "data": [
        {
            "id": 1,
            "email": "apiuser4@mail.com",
            "username": "apiuser4",
            "created_at": "2021-11-02 11:44:20"
        },
        {
            "id": 2,
            "email": "testapiuser@mail.com",
            "username": "testapiuser",
            "created_at": "2021-11-02 11:46:57"
        },
        {
            "id": 3,
            "email": "testapiuser2@mail.com",
            "username": "testapiuser2",
            "created_at": "2021-11-02 12:07:54"
        }
    ],
    "links": {
        "first": "https://members.4sd.com/api/affiliate/user?page=1",
        "last": "https://members.4sd.com/api/affiliate/user?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "https://members.4sd.com/api/affiliate/user",
        "per_page": 10,
        "to": 3,
        "total": 3
    }
}
```
### Listing transactions
You can also list all successful transactions made my users registered with your affiliate api_key

Example request:

```
curl --location --request GET 'https://members.4sd.com/api/affiliate/transaction?page=1' \
--header 'x-api-key: {{your_api_key}}'
```

Example response:
```json
{
    "data": [
        {
            "id": 15378,
            "user_id": 106163,
            "status": "COMPLETED",
            "amount": "169.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:13:06"
        },
        {
            "id": 15377,
            "user_id": 106163,
            "status": "COMPLETED",
            "amount": "289.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:08:51"
        },
        {
            "id": 15376,
            "user_id": 106162,
            "status": "COMPLETED",
            "amount": "169.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:07:18"
        },
        {
            "id": 15375,
            "user_id": 106162,
            "status": "COMPLETED",
            "amount": "289.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:04:31"
        },
        {
            "id": 15374,
            "user_id": 106162,
            "status": "COMPLETED",
            "amount": "169.00",
            "currency": "USD",
            "created_at": "2021-11-02 11:47:56"
        }
    ],
    "links": {
        "first": "https://members.4sd.com/api/affiliate/transaction?page=1",
        "last": "https://members.4sd.com/api/affiliate/transaction?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "https://members.4sd.com/api/affiliate/transaction",
        "per_page": 10,
        "to": 5,
        "total": 5
    }
}
```


### Listing transactions per user
You can also list all successful transactions made by specific user

Example request:
```
curl --location --request GET 'https://members.4sd.com/api/affiliate/user/106163/transaction?page=1' \
--header 'x-api-key: {{your_api_key}}'
```

Example response

```json
{
    "data": [
        {
            "id": 15378,
            "user_id": 106163,
            "status": "COMPLETED",
            "amount": "169.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:13:06"
        },
        {
            "id": 15377,
            "user_id": 106163,
            "status": "COMPLETED",
            "amount": "289.00",
            "currency": "USD",
            "created_at": "2021-11-02 12:08:51"
        }
    ],
    "links": {
        "first": "https://members.4sd.com/api/affiliate/user/106163/transaction?page=1",
        "last": "https://members.4sd.com/api/affiliate/user/106163/transaction?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "https://members.4sd.com/api/affiliate/user/106163/transaction",
        "per_page": 10,
        "to": 2,
        "total": 2
    }
}
```
