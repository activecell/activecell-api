Churn Forecast
==============

> ** quote **
>
> -Source

Your company's churn forecast is a plan--albeit a tragic one--for how many customers you will lose each period. The reality is, most customers don't last forever, but understanding their attrition rate and whether that varies by customer segment is one of the most important drivers of robust health for a business.

As with all forecasts, the forecast assumptions are tied to a scenario, and the time periods are not constrained to the future. Leave your historical plans in place to conduct plan vs. actual analysis as you iterate and improve!


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the churn forecast record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* period_id [String] A system-defined BSON ObjectId identifier for the period
* segment_id [String] A system-defined BSON ObjectId identifier for the segment
* churn_forecast [Integer] The planned customer churn for that segment and period

Note for Aleksey: Does it make sense to consider sending Array JSON vs Verbose JSON for potentially large feeds like this? Let's discuss...

Get churn forecast
----------------------

* `GET /churn_forecast.json` will return the churn forecast for the company in the application's date range scope.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "churn_forecast": 72
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "77cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "churn_forecast": 91
  },
  {
    "id": "87cc67093475061e3d95369d",
    "scenario_id": "97cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "segment_id": "57cc67093475061e3d95369d",
    "churn_forecast": 32
  }
]
```

Aleksey: Alternatively, we could send and receive Array JSON:

```json
[
  [
    "17cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    72
  ],
  [
    "67cc67093475061e3d95369d",
    "77cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    91
  ],
  [
    "87cc67093475061e3d95369d",
    "97cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    32
  ]
]
```


Update churn forecast
-------------------------

* `PUT /churn_forecast/17cc67093475061e3d95369d.json` will update the churn history from the parameters passed.

```json
{
  "churn_forecast": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the churn forecast in the response body. If the user does not have access to update the churn forecast, you'll see `403 Forbidden`. See the **Get churn forecast** endpoint for more info.


Create and delete churn forecast
-------------------------------------

There is no mechanism for creating and destroying churn forecast records. A complete matrix is maintained automatically, and until a history is entered, the churn forecast is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
