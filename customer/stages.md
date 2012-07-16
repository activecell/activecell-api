Customer Acquisition Stages
=================

> **Quote.**  
>
> -Source

Regrettably, customers typically don't show up out of the clear blue sky. In most business models, there is a customer acquisition funnel with multiple "stages" in process. Only a portion of potential customers in one stage reach the next stage, and sometimes there is a "lag period" during the sales/marketing cycle.

For example, in a traditional sales model, businesses encounter Prospects, some portion of whom become Leads, and some portion of Leads actually become Customers. For web traffic, businesses often see Visitors, some portion of whom become Trials, some portion of whom become Customers.

By tracking the conversion across these key stages, it is possible to optimize your customer acquisition process, particularly across different channels.

Fields
------

* id [String] A system-defined BSON ObjectId identifier for the stage
* name [String] The name of the stage (user-defined)
* position [Integer] An integer to indicate the order of the stages
  * Each of a company's stages must have a different position, though they do not have to be consecutive
* lag_periods [Integer] An optional number of periods indicating how long it takes on average for a potential customer to reach the next stage (0 by default)


Get stages
------------

* `GET /stages.json` will return the all the stages for the company. There is no pagination because we currently limit companies to 50 stages (more than 10 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Prospect",
    "position": 1,
    "lag_periods":1
  },
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Lead",
    "position": 2,
    "lag_periods":0
  },
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Customer",
    "position": 3,
    "lag_periods":0
  }
]
```


Get stage
-----------

* `GET /stages/1.json` will return the specified stage

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Prospect",
  "position": 1,
  "lag_periods":1
}
```


Create stage
--------------

* `POST /stages.json` will create a new stage from the parameters passed.

```json
{
  "name": "Prospect",
  "position": 1,
  "lag_periods":1
}
```

Lag periods will default to 0 if not provided. Position must be provided and must not conflict with an existing company stage.

This will return `201 Created`, with the location of the new stage in the `Location` header along with the current JSON representation of the stage if the creation was a success. See the **Get stage* endpoint for more info.


Update stage
--------------

* `PUT /stages/27cc67093475061e3d95369d.json` will update the stages from the parameters passed.

```json
{
  "name": "Prospect",
  "position": 1,
  "lag_periods":1
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the stage in the response body. If the user does not have access to update the stage, you'll see `403 Forbidden`. See the **Get stage** endpoint for more info.


Delete stage
-------------

* `DELETE /stages/17cc67093475061e3d95369d.json` will delete the stage specified and return `204 No Content` if that was successful. If the user does not have access to delete the stage, you'll see `403 Forbidden`.

Note: At least one stage must exist for a company, so an attempt to delete the last remaining stage will return `403 Forbidden` as well.