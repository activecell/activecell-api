Customer Segments
=================

> **This job would be great if it weren't for the $&@^#@ customers.**
> **Which ones?**
> **All of them.**
>
> -Clerks

Not all of your customers are stars. You may be losing money on some of your customers, sometimes on purpose and sometimes not. Some customers are in for the long haul, and some customers come and go. The important part is knowing which are which, and managing your business accordingly.




Fields
------

* id [String] A system-defined BSON ObjectId identifier for the segment
* name [String] The name of the segment (user-defined)


Get segments
------------

* `GET /segments.json` will return the all the segments for the company. There is no pagination because we currently limit companies to 50 segments (more than 10 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Platinum"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Gold"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Silver"
  }
]
```


Get segment
-----------

* `GET /segments/1.json` will return the specified segment

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Platinum"
}
```


Create segment
--------------

* `POST /segments.json` will create a new segment from the parameters passed.

```json
{
  "name": "Platinum"
}
```

This will return `201 Created`, with the location of the new segment in the `Location` header along with the current JSON representation of the segment if the creation was a success. See the **Get segment* endpoint for more info.


Update segment
--------------

* `PUT /segments/27cc67093475061e3d95369d.json` will update the segments from the parameters passed.

```json
{
  "name": "Silver"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the segment in the response body. If the user does not have access to update the segment, you'll see `403 Forbidden`. See the **Get segment** endpoint for more info.


Delete segment
-------------

* `DELETE /segments/17cc67093475061e3d95369d.json` will delete the segment specified and return `204 No Content` if that was successful. If the user does not have access to delete the segment, you'll see `403 Forbidden`.

Note: At least one segment must exist for a company, so an attempt to delete the last remaining segment will return `403 Forbidden` as well.