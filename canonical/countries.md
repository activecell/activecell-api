Industries
========

> **This country needs more than a building right now. 
> It needs hope.**
>
> -V for Vendetta

We maintain a canonical list of countries so that you can select the one you are from.

Why select your country from the list? We keep simple demographic data about our customers, and it's very helpful to know where our biggest concentrations of customers are so we can prioritize their needs.


Fields
------

* id [String] A BSON ObjectId Datatype identifier for the country (system-defined)
* name [String] The name of the country


Get countries
------------

* `GET /countries.json` will return our canonical list of countries. There is no pagination because we curate the list and keep in short.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "United States"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Canada"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "United Kingdom"
  }
]
```
