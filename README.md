# Firmwater LMS API

This is the API for Firmwater LMS (lms.firmwater.com). It is a REST-style API that uses JSON serialization and requires HTTPS access.

### Base URL

All documented endpoints are relative to a base HTTPS URL. The default base URL is:

    https://lms.firmwater.com/api

Organizations with custom domains will have a similar base URL using their custom domain. For instance, an organization with the domain `example.com` would use the following base URL:

    https://example.com/api

### Authentication

At the moment, the API can only be accessed via a browser while logged into Firmwater LMS.

### Making Requests

The API relies on content negotiation to determine the send/receive formats and the expected API version. Currently, all client requests should include the `Accept: application/vnd.firmwater+json` header. The API will always respond with a `Content-Type: application/json; charset=utf-8 ` header.

# API Reference

A number of APIs are exposed for different resources. This section describes available APIs.

# Current User API

The current user API will provide access to resources corresponding to the currently authenticated user. It is a convenient way of accessing many of the resources exposed by the users API for the currently logged in user.

## Get the authenticated user

    GET /user

### Response

```
Status: 200 OK
{
  "id": "0f8fad5b-d9cb-469f-a165-70867728950e",
  "clientId": "firmwater",
  "username": "mpareja@firmwater.com",
  "firstName": "Mario",
  "middleName": "",
  "lastName": "Pareja",
  "emailAddress": "mpareja@firmwater.com",
  "preferredLanguage": "en",
  "externalId": "id_from_other_system",
  "photoUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/123_kl3jk2kj.png",
  "photoThumbnailUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/123_thumb_kl3jk2kj.png.jpg",
  "residencePhone": null,
  "businessPhone": null,
  "mobilePhone": null,
  "dateOfBirth": null,
  "expiryDateTime": "2014-01-14T04:33:35Z",
}
```

## Get training session information for the authenticated user

    GET /user/training/sessions/{trainingSessionId}

### Response

```
Status: 200 OK
{
  "id": "0bbbbbbb-d9cb-469f-a165-70867728950e",
  "user": {
    "id": "0f8fad5b-d9cb-469f-a165-70867728950e",
    "clientId": "firmwater",
    "username": "mpareja@firmwater.com",
    "firstName": "Mario",
    "middleName": "",
    "lastName": "Pareja",
    "emailAddress": "mpareja@firmwater.com",
    "preferredLanguage": "en",
    "externalId": "id_from_other_system",
    "photoUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/123_kl3jk2kj.png",
    "photoThumbnailUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/123_thumb_kl3jk2kj.png.jpg",
    "residencePhone": null,
    "businessPhone": null,
    "mobilePhone": null,
    "dateOfBirth": null,
    "expiryDateTime": "2014-01-14T04:33:35Z",
  },
  "item": {
    "id": "0ddddddd-d9cb-469f-a165-70867728950e",
    "externalId": "intro"
  },
  "attempt": {
    "id": "0eeeeeee-d9cb-469f-a165-70867728950e"
  }
}
```

## Retrieve notices to be delivered to the authenticated user

    GET /user/notices

### Response

```
Status: 200 OK
[
  {
    "id":"e835c4df-7bac-442e-ba91-17f4593dffed",
    "type":"OneTime",
    "message":"<blink>This blinking message will be shown once.</blink>",
    "cssClass":"warning",
    "user": {
      "id": "ae5d8b42-0110-47d6-9ad9-60f4956c12ec"
    }
  },
  {
    "id":"f835c4df-7bac-442e-ba91-17f4593dffed",
    "type":"Persistent",
    "message":"This message will be shown until the user dismisses it.",
    "cssClass":"warning",
    "user": {
      "id": "ae5d8b42-0110-47d6-9ad9-60f4956c12ec"
    }
  }
]
```

## Dismiss a notice delivered to the authenticated user

    DELETE /user/notices/{noticeId}

### Response

```
Status: 204 No Content
```

# In App Notice API

The in app notice API will provide access to resources for communicating with users via the LMS user interface.

## Retrieve notices to be delivered to a user

    GET /{clientId}/notices/users/{userId}

### Response

```
Status: 200 OK
[
  {
    "id":"e835c4df-7bac-442e-ba91-17f4593dffed",
    "type":"OneTime",
    "message":"<blink>This blinking message will be shown once.</blink>",
    "cssClass":"warning",
    "user": {
      "id": "ae5d8b42-0110-47d6-9ad9-60f4956c12ec"
    }
  },
  {
    "id":"f835c4df-7bac-442e-ba91-17f4593dffed",
    "type":"Persistent",
    "message":"This message will be shown until the user dismisses it.",
    "cssClass":"warning",
    "user": {
      "id": "ae5d8b42-0110-47d6-9ad9-60f4956c12ec"
    }
  }
]
```

## Queue a notice to be delivered to a user

    POST /{clientId}/notices/users/{userId}

```
{
  "type":"OneTime",
  "messageText":"This is a <a>test</a> OneTime notice.",
  "cssClass":"warning"
}
```

### Response

```
{
  "id":"e835c4df-7bac-442e-ba91-17f4593dffed",
  "type":"OneTime",
  "message":"This is a &lt;a&gt;test&lt;/a&gt; OneTime notice.",
  "cssClass":"warning"
  "user": {
    "id": "ae5d8b42-0110-47d6-9ad9-60f4956c12ec"
  }
}
```

## Dismiss a notice to be delivered to a user

    DELETE /{clientId}/notices/users/{noticeId}

### Response

```
Status: 204 No Content
```

# Users API

The users API will provide access to resources corresponding to users.

## Get a single user

    GET /{clientId}/users/{userId}

### Response

```
Status: 200 OK
{
  "id": "0f8fad5b-d9cb-469f-a165-70867728950e",
  "clientId": "firmwater",
  "username": "mpareja@firmwater.com",
  "firstName": "Mario",
  "middleName": "",
  "lastName": "Pareja",
  "emailAddress": "mpareja@firmwater.com",
  "preferredLanguage": "en",
  "externalId": "id_from_other_system",
  "photoThumbnailUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/123_thumb_kl3jk2kj.png.jpg",
  "expiryDateTime": "2014-01-14T04:33:35Z",
  "residencePhone": null,
  "businessPhone": null,
  "mobilePhone": null
}
```
