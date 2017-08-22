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

`POST /users/token`

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

`POST /users/add`


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

`POST /users/edit`


# Events

## List 

>Response:

```json
{
    "success": true,
    "data": {
        "events": [
            {
                "id": "0d1b0b21-7bcb-4458-a777-d48c98c5cfb2",
                "name": "Empreendedorismo de Palco",
                "date_start": "2017-08-19T19:47:23+00:00",
                "date_end": "2017-08-08T00:00:00+00:00",
                "tags": "",
                "type": "Symposium",
                "price": 0,
                "published": true,
                "active": true,
                "user": {
                    "id": "e763e5ab-93c3-4bdb-92d9-7b3d9e269498",
                    "group_id": 1,
                    "username": "brunoserrabr@gmail.com",
                    "name": "Bruno Serra",
                    "birthdate": "2017-08-11T14:13:10+00:00",
                    "tags": "",
                    "active": 1,
                    "deleted": null
                }
            }
        ]
    },
     "pagination": {
         "finder": "all",
         "page": 1,
         "current": 1,
         "count": 1,
         "perPage": 20,
         "prevPage": false,
         "nextPage": false,
         "pageCount": 1,
         "sort": null,
         "direction": false,
         "limit": null,
         "sortDefault": false,
         "directionDefault": false,
         "scope": null
     }
}
```

### HTTP Request

`get /events`


## Add

>Request:

```json
{
	"name": "Meu Evento",
	"date_start": "2017-08-25 00:00:00",
	"date_end": "2017-08-29 00:00:00",
	"type": "2",
	"price": 345.0
}
```

>Response:

```json
{
    "success": true,
    "data": {
        "event": {
            "id": "dc249732-0422-4e09-86de-535898f11bae"
        }
    }
}
```

### HTTP Request

`POST /events/add`


# Event Activities

## Add 

>Request:

```json
{
	"name": "My Event Activity",
	"description": "Lorem Ipsum dollor sit amet",
	"price": 300,
	"type": 1,
	"start_at": "2017-08-25 09:00:00",
	"end_at": "2017-08-25 11:59:00",
	"speaker_id": "a7091517-eadb-4a7e-9fb9-1acae8ef47bb",
	"event_place_id": "041a746d-2ca7-4597-b8d5-e1d67b8f20d0"
}
```

>Response:

```json
{
    "success": true,
    "data": {
        "activity": {
            "event_id": "dc249732-0422-4e09-86de-535898f11bae",
            "name": "My Event Activity",
            "description": "Lorem Ipsum dollor sit amet",
            "price": 300,
            "type": "Lecture",
            "start_at": "2017-08-25T09:00:00+00:00",
            "end_at": "2017-08-25T11:59:00+00:00",
            "speaker_id": "a7091517-eadb-4a7e-9fb9-1acae8ef47bb",
            "event_place_id": "041a746d-2ca7-4597-b8d5-e1d67b8f20d0",
            "id": "b1668b10-203f-4382-9183-31ca586331f6"
        }
    }
}
```

### HTTP Request

`POST /activities/add/<event_id>`


## Activity Types

>Response:

```json
{
    "success": true,
    "data": {
        "types": {
            "1": "Lecture",
            "2": "Workshop",
            "3": "Discussion Panel",
            "4": "Spare Time"
        }
    }
}
```

### HTTP Request

`GET /activities/types`
