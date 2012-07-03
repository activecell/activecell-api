Revenue Streams
===============

> **In this country, you gotta make the money first.  
> Then when you get the money, you get the power.  
> Then when you get the power, then you get the women.**
>
> -Scarface

Revenue streams are essentially categories of specific products & services. In some businesses, revenue streams as referred to as "business lines" or "service areas." Most often, revenue streams correspond to one or more revenue accounts in the chart of accounts. In larger organizations, they can correspond with departments or business units, but let's not get ahead of ourselves!

For users who connect to QuickBooks, all income accounts will be added as revenue streams automatically, but future revenue streams can be added manually for planning


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the revenue stream
* name [String] The name of the stream (user-defined or imported from QuickBooks)


Get streams
------------

* `GET /streams.json` will return the all the revenue streams for the company. There is no pagination because we currently limit companies to 50 streams (more than 10 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Professional services"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Media purchases"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Event revenue"
  }
]
```


Get stream
-----------

* `GET /streams/17cc67093475061e3d95369d.json` will return the specified stream and its forecast channel/segment mix

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Professional services",
	"unit revenue forecast":[
		{
		  "scenario_id":"27cc67093475061e3d95369d", 
		  "segment_id":"37cc67093475061e3d95369d", 
		  "unit\_revenue_forecast":100
		},
		{
		  "scenario_id":"27cc67093475061e3d95369d", 
		  "segment_id":"57cc67093475061e3d95369d", 
		  "unit\_revenue_forecast":200
		  },
		{
		  "scenario_id":"27cc67093475061e3d95369d", 
		  "segment_id":"77cc67093475061e3d95369d",
		  "unit\_revenue_forecast":300
		}
	]
}
```


Create stream
--------------

* `POST /streams.json` will create a new revenue stream from the parameters passed.

```json
{
  "name": "Event revenue"
}
```

This will return `201 Created`, with the location of the new stream in the `Location` header along with the current JSON representation of the stream if the creation was a success. See the **Get channel* endpoint for more info.


Update stream
--------------

* `PUT /streams/27cc67093475061e3d95369d.json` will update the stream from the parameters passed.

```json
{
  "name": "Karate lessons"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the stream in the response body. If the user does not have access to update the stream, you'll see `403 Forbidden`. See the **Get stream** endpoint for more info.


Delete stream
-------------

* `DELETE /streams/27cc67093475061e3d95369d.json` will delete the stream specified and return `204 No Content` if that was successful. If the user does not have access to delete the stream, you'll see `403 Forbidden`.

Note: At least one revenue stream must exist for a company, so an attempt to delete the last remaining revenue stream will return `403 Forbidden` as well.