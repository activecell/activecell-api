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
* conversion_forecast [Integer] The planned volume of customers for that channel, stage, and period


Get conversion forecast
----------------------

* `GET /conversion_forecast.json` will return the conversion forecast for the company in the application's date range scope.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "stage_id": "47cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "conversion_forecast": 72
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "77cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "stage_id": "47cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "conversion_forecast": 91
  },
  {
    "id": "87cc67093475061e3d95369d",
    "scenario_id": "97cc67093475061e3d95369d",
    "period_id": "37cc67093475061e3d95369d",
    "stage_id": "47cc67093475061e3d95369d",
    "channel_id": "57cc67093475061e3d95369d",
    "conversion_forecast": 32
  }
]
```


Update conversion forecast
-------------------------

* `PUT /conversion_forecast/17cc67093475061e3d95369d.json` will update the conversion history from the parameters passed.

```json
{
  "conversion_forecast": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the conversion forecast in the response body. If the user does not have access to update the conversion forecast, you'll see `403 Forbidden`. See the **Get conversion forecast** endpoint for more info.


Create and delete conversion forecast
-------------------------------------

There is no mechanism for creating and destroying conversion records. A complete matrix is maintained automatically, and until a history is entered, the conversion rate is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
