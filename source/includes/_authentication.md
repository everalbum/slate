# Authentication

<aside class="notice">
An `auth_token` is required to use the Everalbum API.
</aside>

There are two ways to get an `auth_token`: <br /><br />
<ul>
  <li>Registering for the first time</li>
  <li>Logging in an existing user</li>
</ul>

Registration and Login requests are detailed below, the response for each of them is the same (a `user` response). The details of that response are below the Registration and Login request examples.

## Registration

`POST http://API_URL/users.json`

> The HTTP Request parameters required for registering a user are:

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "johndoe@email.com",
  "password": "pa$$w0rd"
}
```

## Login

`POST http://API_URL/users/sign_in.json`


```json
{
  "email": "johndoe@email.com",
  "password": "pa$$w0rd"
}
```

## User Authentication Response

```json
{
    "auth_token": "GYbny3Q9Toak34Kxqd4Q",
    "created_at": "2016-01-01T12:59:30Z",
    "email": "johndoe@email.com",
    "email_provider": null,
    "fb_access_token": null,
    "fb_id": null,
    "features": [
        "free_space_push",
        "detect_faces",
        "welcome_email",
        "new_photos_push",
        "detour_upload",
        "upload_videos",
        "recent_photos_email",
        "album_clustering",
        "throwbacks",
        "nps_followup_email",
        "initial_backup_email"
    ],
    "first_name": "John",
    "id": 256,
    "last_name": "Doe",
    "locale": null,
    "permissions":     {
        "upload_originals": false,
        "upload_videos": false
    },
    "phone_number": null,
    "photo_limit": null,
    "referral_token": "f619f420",
    "role": "basic",
    "timezone": null
}
```

This response is returned whenever a user is successfully authenticated against the Everalbum API.

As you can see, there are a lot of properties in this response. The one you'll be most interested in is `auth_token`

You'll want to store the `auth_token`. The API expects the `auth_token` to be included in all requests.

You can specify the user's `auth_token` in one of two ways.

## Authenticating API Calls

### Query Parameter
```shell
# Appended to the URL as a query parameter
https://API_URL/:endpoint.json?auth_token=AUTH_TOKEN
```
You can append the authenticated user's `auth_token` to each URL per the API request


### Request Header
```shell
# HTTP Header
Authorization: TBD - needs documentation
```
You can also send the `auth_token` as an HTTP Request Header
