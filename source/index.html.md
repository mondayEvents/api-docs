---
title: Eventos.ninja API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='http://eventos.ninja'>Eventos.ninja &copy; 2017</a>

includes:
  - errors

search: true
---

# Introduction

<aside class="warning">
Under development
</aside>

The eventos.ninja API provides all functionality and data needed to interact with the evento.ninja’s ecosystem.
With this API you are able to:

* List available events
* Search for events based on tags
* Signup a user
* Get user’s related information (personal info, registered events, created events)
* Create an event as a user (with all relational data, such as: event managers and activities)
* Register to an event (and also cancel the registration)
* List registered users to user's event
* Purchase through the checkout API
* Manage event registrations

# Users

## Authentication

```json
{
	"username": "email",
	"password": "password"
}
```

>Response:

```json
{
    "success": true,
    "JWT": "eyJ0eXAiOi...R5d0eOLIcEbjVooXnjuwmW-XOJQPVAwtUk",
    "data": {
        "user": {
            "id": "e763e5ab-93c3-4bdb-92d9-7b3d9e269498",
            "username": "loremipsum@gmail.com",
            "name": "Lorem Ipsum",
            "birthdate": "2015-08-25T00:00:00+00:00",
            "tags": "",
            "active": 1,
            "deleted": null
        }
    }
}
```

Most functionalities requeries the user to be logged. To authenticate an user send a JSON to get a Bearer token.

### HTTP Request

`POST http://example.com/users/token`

## Signup

<aside class="notice">
Authentication header is not required
</aside>

```json
{
	"name": "Lorem Ipsum",
	"username": "loremipsum@gmail.com",
	"password": "password",
	"birthdate": {
		"day": "25",
		"month": "08",
		"year": "1992",
		"minute": "00",
		"hour": "00"
	}
}
```
>Response:

```json
{
    "success": true,
    "JWT": "eyJ0eXAiOiJKV...4UoXwk-b2dZew25-E8v4M",
    "data": []
}
```


### HTTP Request

`POST http://example.com/users/add`


## Update

Send a JSON only with the information to be updated

```json
{
	"name": "Lorem Ipsum",
	"username": "loremipsum@gmail.com", // must be unique
	"password": "password",
	"birthdate": {
		"day": "25",
		"month": "08",
		"year": "1992",
		"minute": "00",
		"hour": "00"
	}
}
```
>Response:

```json
{
    "success": true,
    "data": []
}
```


### HTTP Request

`POST http://example.com/users/edit`