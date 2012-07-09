Timesheet Summary
=================

> ** quote **
>
> -Source

Your company's timesheet history may be either:

1. Output from an actual time tracking system, or 
1. An informal estimate of the amount of time each employee spends on a mix of activities and customers

In either case, the value of the historical data is paramount to evaluating the effectiveness of your investments in human capital.

The timesheet summary is an aggregate of all the individual transactions that occur for a given period, activity, product, customer, and employee. Most transactions will not have all dimensions populated, and so blank (or "null") values are to be expected for some of these dimensions in each record supplied. Time is expressed simply in minutes. Where the source data has provided hours, these figures have been multiplied by 60.


Fields
------

* period_id [String] A system-defined BSON ObjectId identifier for the period
* employee\_activity_id [String] A system-defined BSON ObjectId identifier for the activity
* product_id [String] A system-defined BSON ObjectId identifier for the product
* customer_id [String] A system-defined BSON ObjectId identifier for the customer
* employee_id [String] A system-defined BSON ObjectId identifier for the employee
* amount_minutes [Integer] The aggregated amount, in minutes

Note for Aleksey: Does it make sense to consider sending Array JSON vs Verbose JSON for potentially large feeds like this? Let's discuss...

Get timesheet summary
---------------------

* `GET /timesheet_summary.json` will return an aggregated summary of timesheet transactions for the company in the application's date range scope.

```json
[
  {
    "period_id": "17cc67093475061e3d95369d",
    "employee\_activity_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "amount_minutes": 120
  },
  {
    "period_id": "77cc67093475061e3d95369d",
    "employee\_activity_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "amount_minutes": 240
  },
  {
    "period_id": "87cc67093475061e3d95369d",
    "employee\_activity_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "amount_minutes": 480
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
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    120
  ],
  [
    "77cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    240
  ],
  [
    "87cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    480
  ]
]
```

