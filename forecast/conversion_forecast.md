Conversion Forecast
=================

> ** quote **
>
> -Source

Your company's conversion forecast is a plan for how many potential customers you will have at each stage in the customer acquisition cycle across each channel. Planning for the conversion funnel is a critical step towards both anticipating future customer volume and planning activities that will drive customer volume to the business in a cost-effective way.

The model does not consider individual customers or leads--that is what CRM and other tracking software is for. The model plans for volume within each stage and channel.

As with all forecasts, the forecast assumptions are tied to a scenario, and the time periods are not constrained to the future. Leave your historical plans in place to conduct plan vs. actual analysis as you iterate and improve!


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the conversion record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* period_id [String] A system-defined BSON ObjectId identifier for the period
* stage_id [String] A system-defined BSON ObjectId identifier for the customer acquisition stage
* channel_id [String] A system-defined BSON ObjectId identifier for the channel
* volume_forecast [Integer] The planned volume of customers for that channel, stage, and period


Get conversion forecast
----------------------

* `GET /conversion_forecast.json` will return the conversion forecast for the company in the application's date range scope.

```json
[
  [
    "17cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    72
  ],
  [
    "67cc67093475061e3d95369d",
    "77cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    91
  ],
  [
    "87cc67093475061e3d95369d",
    "97cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    32
  ]
]
```

**Critical JSON Array note:** Due to the potential size of these datasets, data is transmitted as a JSON Array rather than the traditional "Verbose" JSON featured throughout most of the API. The order of the fields reflects the order in the "Fields" section of this document.


Update conversion forecast
-------------------------

* `PUT /conversion_forecast/17cc67093475061e3d95369d.json` will update the conversion history from the parameters passed.

```json
{
  "volume_forecast": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the conversion forecast in the response body. If the user does not have access to update the conversion forecast, you'll see `403 Forbidden`. See the **Get conversion forecast** endpoint for more info.


Create and delete conversion forecast
-------------------------------------

There is no mechanism for creating and destroying conversion records. A complete matrix is maintained automatically, and until a history is entered, the conversion rate is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
