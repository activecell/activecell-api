Revenue Streams
========

> **Quotes are a great idea.**
>
> - Adam Neary

Revenue streams are essentially categories of specific products & services. In some businesses, revenue streams as referred to as "business lines" or "service areas." Most often, revenue streams correspond to one or more revenue accounts in the chart of accounts. In larger organizations, they can correspond with departments or business units, but let's not get ahead of ourselves!


Get streams
------------

* `GET /streams.json` will return the all the revenue streams for the company. There is no pagination because we currently limit companies to 50 streams (more than 10 is rare!).

```json
[
  {
    "id": 1,
    "name": "Professional services"
  },
  {
    "id": 2,
    "name": "Media purchases"
  },
  {
    "id": 3,
    "name": "Event revenue"
  }
]
```


Get stream
-----------

* `GET /streams/1.json` will return the specified stream and its forecast channel/segment mix

```json
{
  "id": 1,
  "name": "Professional services",
  "commission": 0,
	"channel-segment mix":[
		{"segment_id":1, "distribution":40},
		{"segment_id":2, "distribution":30},
		{"segment_id":3, "distribution":30}
	]
}
```


Create channel
--------------

* `POST /channels.json` will create a new channel from the parameters passed.

```json
{
  "name": "Affiliate sales",
  "commission": 10,
	"channel-segment mix":[
		{"segment_id":1, "distribution":60},
		{"segment_id":2, "distribution":40}
	]
}
```

Commission will default to 0% if not provided. Channel/segment mix will allocate 100% to the first segment if not provided. If provided, the sum of channel/segment mix must equal 100.

This will return `201 Created`, with the location of the new channel in the `Location` header along with the current JSON representation of the channel if the creation was a success. See the **Get channel* endpoint for more info.


Update channel
--------------

* `PUT /channels/2.json` will update the channels from the parameters passed.

```json
{
  "name": "Direct sales",
  "commission": 25,
	"channel-segment mix":[
		{"segment_id":1, "distribution":100}
	]
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the channel in the response body. If the user does not have access to update the channel, you'll see `403 Forbidden`. See the **Get channel** endpoint for more info.


Delete channel
-------------

* `DELETE /channels/1.json` will delete the channel specified and return `204 No Content` if that was successful. If the user does not have access to delete the channel, you'll see `403 Forbidden`.

Note: At least one revenue stream must exist for a company, so an attempt to delete the last remaining revenue stream will return `403 Forbidden` as well.