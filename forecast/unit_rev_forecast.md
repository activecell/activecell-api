Unit Revenue Forecast
=====================

> ** quote **
>
> -Source

Unit economics are a key component of planning and analysis. A unit revenue forecast, put simply, is how much revenue you can expect to earn from a single customer per period. Across each of your customer segments, you can plan for the mix of revenue across your various revenue streams. It is this unit revenue planning, coupled with the customer volume forecast, that builds a smart forecast for revenue, building block by building block.

As with all forecasts, the forecast assumptions are tied to a scenario. Dollar values are expressed as integers in cents, so be certain to convert to dollars by dividing by 100.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the churn forecast record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* segment_id [String] A system-defined BSON ObjectId identifier for the customer segment
* stream_id [String] A system-defined BSON ObjectId identifier for the revenue stream
* unit\_rev_forecast [Integer] The planned unit revenue for that segment and stream, in USD converted to cents (divided by 100)


Get unit revenue forecast
----------------------

* `GET /unit_rev_forecast.json` will return the unit revenue forecast for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "stream_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "unit_rev_forecast": 4999
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "77cc67093475061e3d95369d",
    "stream_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "unit_rev_forecast": 9999
  },
  {
    "id": "87cc67093475061e3d95369d",
    "scenario_id": "97cc67093475061e3d95369d",
    "stream_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "unit_rev_forecast": 14999
  }
]
```


Update unit revenue forecast
-------------------------

* `PUT /unit_rev_forecast/17cc67093475061e3d95369d.json` will update the unit revenue forecast from the parameters passed.

```json
{
  "unit_rev_forecast": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the unit revenue forecast in the response body. If the user does not have access to update the unit revenue forecast, you'll see `403 Forbidden`. See the **Get unit revenue forecast** endpoint for more info.


Create and delete unit revenue forecast
-------------------------------------

There is no mechanism for creating and destroying unit revenue forecast records. A complete matrix is maintained automatically, and until a history is entered, the unit revenue forecast is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
