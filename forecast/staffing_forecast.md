Staffing Forecast
=================

> ** quote **
>
> -Source

p1

p2


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the staffing forecast record
* scenario_id [String] A system-defined BSON ObjectId identifier for the scenario
* employee\_type_id [String] A system-defined BSON ObjectId identifier for the employee type
* occurrence [String] Specifies how the forecast should be calculated (see valid types below)
* occurrence_month [Integer] If annual occurrence, occurrence\_month specifies in which month the annual event occurs
* occurrence_period [String] A system-defined BSON ObjectId identifier for the period in which the one-time event occurs if fixed occurrence
* fixed_delta [Integer] The change (positive or negative) in the number of employees planned for that employee type in that period. Valid if occurrence is Monthly, Annually, or Fixed.
* revenue_threshold [Integer] The level of revenue corresponding to 1 employee, in USD converted to cents (divided by 100), if occurrence is 'Revenue Threshold'

**Valid occurrence types:**

* '**Monthly**' indicates that the employee count for that type will change regularly each month by a fixed number
* '**Annually**' indicates that the employee count for that type will change regularly each year by a fixed number (in this case, occurrence_month must be populated to specify in which month the annual event occurs)
* '**Fixed**' indicates that the employee count for that type will change by a fixed number within a fixed period (in this case, occurrence_period must be populated to specify in which period the one-time event occurs)
* '**Revenue Threshold**' indicates that for every _$x_ in revenue, 1 employee of that type will be required, and the staffing forecast scales automatically as the revenue forecast shifts  


Get staffing forecasts
-----------------------

* `GET /staffing_forecasts.json` will return the staffing forecasts for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "employee_type_id": "37cc67093475061e3d95369d",
    "occurrence": "Monthly",
    "fixed_delta":1
  },
  {
    "id": "47cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "employee_type_id": "57cc67093475061e3d95369d",
    "occurrence": "Annually",
    "occurrence_month": 1,
    "fixed_delta":2
  },
  {
    "id": "67cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "employee_type_id": "77cc67093475061e3d95369d",
    "occurrence": "Fixed",
    "occurrence_period": "87cc67093475061e3d95369d",
    "fixed_delta":3
  },
  {
    "id": "97cc67093475061e3d95369d",
    "scenario_id": "27cc67093475061e3d95369d",
    "employee_type_id": "07cc67093475061e3d95369d",
    "occurrence": "Revenue Threshold",
    "revenue_threshold": 10000000
  }
]
```


Get staffing forecast
---------------------

* `GET /staffing_forecasts/17cc67093475061e3d95369d.json` will return an individual staffing forecast item

```json
{
  "id": "17cc67093475061e3d95369d",
  "scenario_id": "27cc67093475061e3d95369d",
  "employee_type_id": "37cc67093475061e3d95369d",
  "occurrence": "Monthly",
  "fixed_delta":1
}
```


Create staffing forecast
------------------------

* `POST /staffing_forecasts.json` will create a new staffing forecast from the parameters passed.

```json
{
  "scenario_id": "27cc67093475061e3d95369d",
  "employee_type_id": "37cc67093475061e3d95369d",
  "occurrence": "Monthly",
  "fixed_delta":1
}
```

This will return `201 Created`, with the location of the new staffing forecast in the `Location` header along with the current JSON representation of the staffing forecast if the creation was a success. See the **Get staffing forecast** endpoint for more info.


Update staffing forecast
-------------------------

* `PUT /staffing_forecasts/17cc67093475061e3d95369d.json` will update the staffing forecast from the parameters passed.

```json
{
  "scenario_id": "27cc67093475061e3d95369d",
  "employee_type_id": "07cc67093475061e3d95369d",
  "occurrence": "Revenue Threshold",
  "revenue_threshold": 10000000
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the staffing forecast in the response body. If the user does not have access to update the staffing forecast, you'll see `403 Forbidden`. See the **Get staffing forecast** endpoint for more info.


Delete channel
-------------

* `DELETE /staffing_forecasts/17cc67093475061e3d95369d.json` will delete the staffing forecast specified and return `204 No Content` if that was successful. If the user does not have access to delete the staffing forecast, you'll see `403 Forbidden`.
