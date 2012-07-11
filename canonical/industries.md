Industries
========

> **If GM had kept up with technology like the computer industry has,
> we would all be driving $25 cars that got 1000 MPG.**
>
> -Bill Gates

We maintain a canonical list of industries which you may select to define your business. We used to have a long list, but everyone asked us to keep it simple and pare it down. Lesson learned! 

Why select your industry from the list? We keep simple demographic data about our customers, and it's very helpful to know where our biggest concentrations of customers are so we can prioritize their needs.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the industry
* name [String] The name of the industry
* suggested_streams [Array of Strings] Suggestions for revenue streams common in the industry
* suggested_channels [Array of Strings] Suggestions for customer channels common in the industry
* suggested_segments [Array of Strings] Suggestions for customer segments common in the industry
* suggested_stages [Array of Strings] Suggestions for customer acquisition stages common in the industry


Get industries
------------

* `GET /api/v1/industries.json` will return our canonical list of industries. There is no pagination because we curate the list and keep in short.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Non-profits"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Services"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Manufacturing"
  }
]
```


Get industry
------------

* `GET /api/v1/industries/27cc67093475061e3d95369d.json` will return the specified industry and suggestions for streams, channels, segments, and stages.

```json
{
  "id": "27cc67093475061e3d95369d",
  "name": "Services",
  "suggested_streams":["Professional services","Support","Product resale"],
  "suggested_channels":["Direct sales","Referral","Search engine marketing","Events","Content marketing"],
  "suggested_segments":["Platinum","Gold","Silver"],
  "suggested_stages":["Prospect","Lead","Customer"]
}
```