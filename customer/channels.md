Customer Channels
=================

> **Put. That coffee. Down.**  
> **Coffee's for closers only.**
>
> -Glengarry Glen Ross

Channels are sources of customers. Informal channels such as "Word of Mouth" should be included, as well as internally managed channels such as "Direct Sales." Channels can optionally have a variable commission associated with them. Finally, channel/segment mix is the forecast distribution of customer segments that a channel will bring in, such as 100% platinum customers or 60/40 one-time and loyalty customers.


Fields
------

Channel: 

* id [String] A system-defined BSON ObjectId identifier for the channel
* name [String] The name of the channel (user-defined)
* commission [Float] A percentage rate to be applied to revenue to calculate commission value
  * The value must be greater than or equal to 0 but _may_ be greater than 1.0
  * _Note: 20% should be represented as 0.2 rather than 20._
* channel-segment mix [Array] An array of channel/segment mix line items (see below)

Channel/segment mix:

* segment_id [String] A system-defined BSON ObjectId identifier for the segment
* distribution [Float] A percentage rate representing the share of inbound channel customers forecasted to the segment

Business rules
--------------

**Every channel must have a forecast "channel/segment mix" that adds to 100%.**
This is the forecast "distribution" of inbound customers across the company's segments. In business terms, an example might be that you expect 100% of your customers from events to be "platinum" customers if your segments are silver/gold/platinum. Or, you might reasonably expect your inbound web traffic to be split 70/30 between free and paid segments.


Get channels
------------

* `GET /channels.json` will return the all the channels for the company. There is no pagination because we currently limit companies to 50 channels (more than 10 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Content marketing",
    "commission": 0,
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Direct sales",
    "commission": 0.2,
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Events",
    "commission": 0,
  }
]
```


Get channel
-----------

* `GET /channels/1.json` will return the specified channel and its forecast channel/segment mix

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Content marketing",
  "commission": 0,
	"channel-segment mix":[
		{"segment_id":"47cc67093475061e3d95369d", "distribution":0.4},
		{"segment_id":"57cc67093475061e3d95369d", "distribution":0.3},
		{"segment_id":"67cc67093475061e3d95369d", "distribution":0.3}
	]
}
```


Create channel
--------------

* `POST /channels.json` will create a new channel from the parameters passed.

```json
{
  "name": "Affiliate sales",
  "commission": 0.1,
	"channel-segment mix":[
		{"segment_id":"47cc67093475061e3d95369d", "distribution":0.6},
		{"segment_id":"57cc67093475061e3d95369d", "distribution":0.4}
	]
}
```

Commission will default to 0% if not provided. Channel/segment mix will allocate 100% to the first segment if not provided. If provided, the sum of channel/segment mix must equal 100.

This will return `201 Created`, with the location of the new channel in the `Location` header along with the current JSON representation of the channel if the creation was a success. See the **Get channel* endpoint for more info.


Update channel
--------------

* `PUT /channels/27cc67093475061e3d95369d.json` will update the channels from the parameters passed.

```json
{
  "name": "Direct sales",
  "commission": 25,
	"channel-segment mix":[
		{"segment_id":"47cc67093475061e3d95369d", "distribution":1}
	]
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the channel in the response body. If the user does not have access to update the channel, you'll see `403 Forbidden`. See the **Get channel** endpoint for more info.


Delete channel
-------------

* `DELETE /channels/17cc67093475061e3d95369d.json` will delete the channel specified and return `204 No Content` if that was successful. If the user does not have access to delete the channel, you'll see `403 Forbidden`.

Note: At least one channel must exist for a company, so an attempt to delete the last remaining channel will return `403 Forbidden` as well.