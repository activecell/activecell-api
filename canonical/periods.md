Periods
=======

> **Okay. Time circuit's on. Flux capacitor, fluxing. 
> Engine running. All right.**
>
> -Back to the Future

We maintain a canonical list of monthly financial periods because it makes the reporting cycle lightning fast. More importantly, financial and timesheet history is generally stored at a lower level of granularity (often daily), but forecasts are generally maintained at a higher level of granularity (monthly or quarterly).

We've made the editorial decision for simplicity that the monthly grain is where the budget will meet the actuals, though in the future we may allow users to select custom periods that better match their business cycle and growth stage. Stay tuned!


Fields
------

* id [String] A BSON ObjectId Datatype identifier for the period (system-defined)
* first_day [Date] The first day in the period


Get periods
-----------

* `GET /periods.json` will return our canonical list of periods. There is no pagination because we curate the list.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "first_day": "2012-01-01"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "first_day": "2012-02-01"  
  },
  {
    "id": "37cc67093475061e3d95369d",
    "first_day": "2012-03-01"
  }
]
```
