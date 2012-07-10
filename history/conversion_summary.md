Conversion Summary
=================

> ** quote **
>
> -Source

Your company's conversion history is a record of how many potential customers you have had at each stage in the customer acquisition cycle across each channel. Maintaining a record of this history is a critical step in evaluating the performance of each channel relative to its cost.

Currently, this data is entered manually through the app or supplied using this API, but in the future connectivity to applications with conversion data--such as salesforce.com or google analytics--will be built and automated.


Fields (order of fields is prescriptive for JSON Array)
-------------------------------------------------------

* id [String] A system-defined BSON ObjectId identifier for the conversion record
* period_id [String] A system-defined BSON ObjectId identifier for the period
* stage_id [String] A system-defined BSON ObjectId identifier for the customer acquisition stage
* channel_id [String] A system-defined BSON ObjectId identifier for the channel
* customer_volume [Integer] The aggregated volume of customers for that channel, stage, and period


Get conversion summary
----------------------

* `GET /conversion_summary.json` will return the conversion history for the company in the application's date range scope.

```json
[
  [
    "17cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    72
  ],
  [
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    91
  ],
  [
    "77cc67093475061e3d95369d",
    "87cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    32
  ]
]
```

**Critical JSON Array note:** Due to the potential size of these datasets, data is transmitted as a JSON Array rather than the traditional "Verbose" JSON featured throughout most of the API. The order of the fields reflects the order in the "Fields" section of this document.


Update conversion summary
-------------------------

* `PUT /conversion_summary/17cc67093475061e3d95369d.json` will update the conversion history from the parameters passed.

```json
{
  "customer_volume": 49
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the conversion summary in the response body. If the user does not have access to update the conversion summary, you'll see `403 Forbidden`. See the **Get conversion summary** endpoint for more info.


Create and delete conversion summary
-------------------------------------

There is no mechanism for creating and destroying conversion records. A complete matrix is maintained automatically, and until a history is entered, the conversion rate is 0. To "create" a record, simply find it and then update it from 0 to whatever the appropriate value is.
