Unit Customer Acquisition Cost Forecast
=======================================

> ** quote **
>
> -Source

Unit economics are a key component of planning and analysis. Unit customer acquisition cost, put simply, is how much expense you can expect to incur to attract a single customer. Across each of your customer channels, what are the various types of costs across different cost categories? It is this unit CAC planning, coupled with the customer volume forecast, that builds a smart customer acquisition budget and an optimized channel mix, step by step.

As with all forecasts, the forecast assumptions are tied to a scenario. Dollar values are expressed as integers in cents, so be certain to convert to dollars by dividing by 100.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the churn forecast record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* channel_id [String] A system-defined BSON ObjectId identifier for the customer channel
* category_id [String] A system-defined BSON ObjectId identifier for the expense category
* unit\_cac_forecast [Integer] The planned unit CAC for that channel and category, in USD converted to cents (divided by 100)


Get unit CAC forecast
----------------------

* `GET /unit_cac_forecast.json` will return the unit CAC forecast for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "category_id": "37cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "unit\_cac_forecast": 4999
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "77cc67093475061e3d95369d",
    "category_id": "37cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "unit\_cac_forecast": 9999
  },
  {
    "id": "87cc67093475061e3d95369d",
    "scenario_id": "97cc67093475061e3d95369d",
    "category_id": "37cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "unit\_cac_forecast": 14999
  }
]
```


Update unit CAC forecast
-------------------------

* `PUT /unit_rev_forecast/17cc67093475061e3d95369d.json` will update the unit CAC forecast from the parameters passed.

```json
{
  "unit\_cac_forecast": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the unit CAC forecast in the response body. If the user does not have access to update the unit CAC forecast, you'll see `403 Forbidden`. See the **Get unit CAC forecast** endpoint for more info.


Create and delete unit CAC forecast
-------------------------------------

There is no mechanism for creating and destroying unit CAC forecast records. A complete matrix is maintained automatically, and until a history is entered, the unit CAC forecast is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
