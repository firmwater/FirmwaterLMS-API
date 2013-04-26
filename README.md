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

The API relies on content negotiation to determine the send/receive formats and the expected API version. Currently, all client requests should include the `Accept: application/vnd.firmwater+json` header. The API will always respond with a `Content-Type: application/json` header.

# API Reference

A number of APIs are exposed for different resources. This section describes available APIs.

# Current User API

The current user API will access to resources corresponding to the currently authenticated user. It is a convenient way of accessing similar resources exposed by the Users API except for the currently logged in user.

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
  "photoUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/sdjads-123.png",
  "expiryDateTime": "2014-01-14T04:33:35Z",
  "residencePhone": null,
  "businessPhone": null,
  "mobilePhone": null
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
	  "photoUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/sdjads-123.png",
	  "expiryDateTime": "2014-01-14T04:33:35Z",
	  "residencePhone": null,
	  "businessPhone": null,
	  "mobilePhone": null
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

# Users API

The users API will provide access resources corresponding to users.

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
  "photoUrl": "https://lms.firmwater.com/lms/licensees/firmwater/photos/g6/sdjads-123.png",
  "expiryDateTime": "2014-01-14T04:33:35Z",
  "residencePhone": null,
  "businessPhone": null,
  "mobilePhone": null
}
```
