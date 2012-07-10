Expense Forecast
================

> ** quote **
>
> -Source

p1

p2


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the expense forecast record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* name [String] An optional descriptive name for the forecast
* category_id [String] A system-defined BSON ObjectId identifier for the category
* occurrence [String] Specifies how the forecast should be calculated (see valid types below)
* occurrence_month [Integer] If annual occurrence, occurrence\_month specifies in which month the annual event occurs
* occurrence_period [String] A system-defined BSON ObjectId identifier for the period in which the one-time event occurs if fixed occurrence
* fixed_cost [Integer] The fixed amount of the expense, in USD converted to cents (divided by 100). Valid if occurrence is Monthly, Annually, or Fixed.
* percent_revenue [Decimal] The percentage of revenue to use for calculating the expense if occurrence is 'Revenue Percent'

**Valid occurrence types: **

* '**Monthly**' indicates that the category will incur a fixed cost each month
* '**Annually**' indicates that the category will incur a fixed cost each year
  * If Annually, occurrence_month must be populated to specify in which month the annual charge occurs
* '**Fixed**' indicates that the category will incur a one-time fixed cost within a fixed period
  * If Fixed, occurrence_period must be populated to specify in which period the one-time charge occurs
* '**Revenue Percent**' indicates that the category will incur a cost scaling with revenue at a given percent. As the revenue forecast shifts, the expense forecast scales with it.
* '**Employee Count**' indicates that the category will incur a fixed cost per employee scaling with overall employee count. As the staffing forecast shifts, the expense forecast scales with it


Get expense forecasts
-----------------------

* `GET /expense_forecasts.json` will return the expense forecasts for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "name":"Utilities",
    "category_id": "37cc67093475061e3d95369d",
    "occurrence": "Monthly",
    "fixed_cost":15000
  },
  {
    "id": "47cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "name":"Holiday party",
    "category_id": "57cc67093475061e3d95369d",
    "occurrence": "Annually",
    "occurrence_month": 12,
    "fixed_cost":200000
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "name":"Office Buildout",
    "category_id": "77cc67093475061e3d95369d",
    "occurrence": "Fixed",
    "occurrence_period": "87cc67093475061e3d95369d",
    "fixed_cost":3100000
  },
  {
    "id": "97cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "name":"Web Hosting",
    "category_id": "07cc67093475061e3d95369d",
    "occurrence": "Revenue Percent",
    "revenue_threshold": 0.000125
  },
  {
    "id": "97cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "name":"Rent of Office Space",
    "category_id": "07cc67093475061e3d95369d",
    "occurrence": "Employee Count",
    "fixed_cost": 50000
  }
]
```


Get expense forecast
---------------------

* `GET /expense_forecasts/17cc67093475061e3d95369d.json` will return an individual expense forecast item

```json
{
  "id": "17cc67093475061e3d95369d",
  "scenario_id": "27cc67093475061e3d95369d",
  "name":"Utilities",
  "category_id": "37cc67093475061e3d95369d",
  "occurrence": "Monthly",
  "fixed_cost":15000
}
```


Create expense forecast
------------------------

* `POST /expense_forecasts.json` will create a new expense forecast from the parameters passed.

```json
{
  "scenario_id": "27cc67093475061e3d95369d",
  "name":"Holiday party",
  "category_id": "57cc67093475061e3d95369d",
  "occurrence": "Annually",
  "occurrence_month": 12,
  "fixed_cost":200000
}
```

This will return `201 Created`, with the location of the new expense forecast in the `Location` header along with the current JSON representation of the expense forecast if the creation was a success. See the **Get expense forecast** endpoint for more info.


Update expense forecast
-------------------------

* `PUT /expense_forecasts/17cc67093475061e3d95369d.json` will update the expense forecast from the parameters passed.

```json
{
  "scenario_id": "27cc67093475061e3d95369d",
  "name":"Office Buildout",
  "category_id": "77cc67093475061e3d95369d",
  "occurrence": "Fixed",
  "occurrence_period": "87cc67093475061e3d95369d",
  "fixed_cost":3100000
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the expense forecast in the response body. If the user does not have access to update the expense forecast, you'll see `403 Forbidden`. See the **Get expense forecast** endpoint for more info.


Delete channel
-------------

* `DELETE /expense_forecasts/17cc67093475061e3d95369d.json` will delete the expense forecast specified and return `204 No Content` if that was successful. If the user does not have access to delete the expense forecast, you'll see `403 Forbidden`.
