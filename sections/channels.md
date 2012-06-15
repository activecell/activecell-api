Channels
========

> Quotes are a great idea. - Adam Neary

What is a channel? Let me tell you in several sentences! What is a channel? Let me tell you in several sentences! What is a channel? Let me tell you in several sentences! What is a channel? Let me tell you in several sentences!

Get channels
------------

* `GET /channels.json` will return the all the channels for the company. There is no pagination because we currently limit companies to 50 channels (more than 10 is rare!).

```json
[
  {
    "id": 1,
    "name": "Content marketing",
    "commission": 0,
  },
  {
    "id": 2,
    "name": "Direct sales",
    "commission": 0.20,
  },
  {
    "id": 3,
    "name": "Events",
    "commission": 0,
  },
]
```

Get channel
-----------

* `GET /channels/1.json` will return the specified channel.

```json
{
  "id": 1,
  "name": "Content marketing",
  "commission": 0
}
```


Create channel
--------------

* `POST /channels.json` will create a new channel from the parameters passed.

```json
{
  "name": "Affiliate sales",
  "commission": 0.10
}
```

This will return `201 Created`, with the location of the new channel in the `Location` header along with the current JSON representation of the channel if the creation was a success. See the **Get channel* endpoint for more info.


Update channel
--------------

* `PUT /channels/2.json` will update the channels from the parameters passed.

```json
{
  "name": "Direct sales",
  "commission": 0.25
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the channel in the response body. If the user does not have access to update the channel, you'll see `403 Forbidden`. See the **Get channel** endpoint for more info.


Delete message
-------------

* `DELETE /channels/1.json` will delete the channel specified and return `204 No Content` if that was successful. If the user does not have access to delete the channel, you'll see `403 Forbidden`.