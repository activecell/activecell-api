Vendors
=======

> **Right.  
> Let's sort the buyers from the spyers, the needy from the greedy, and those who trust me from the ones who don't.  
> 'Cause if you can't see value here today, you're not up here shopping. You're up here shoplifting.**
>
> -Lock, Stock, and Two Smoking Barrels


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the vendor
* name [String] The name of the vendor (user-defined or imported from QuickBooks)


Get vendors
------------

* `GET /vendors.json` will return the all the vendors for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Big Media Co."
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Madison Avenue Properties"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Winston's Cigars"
  }
]
```


Get vendor
-----------

* `GET /vendors/17cc67093475061e3d95369d.json` will return the specified vendor

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Big Media Co."
}
```


Create vendor
--------------

* `POST /vendors.json` will create a new vendor from the parameters passed.

```json
{
  "name": "Big Media Co."
}
```

This will return `201 Created`, with the location of the new vendor in the `Location` header along with the current JSON representation of the vendor if the creation was a success. See the **Get channel* endpoint for more info.


Update vendor
--------------

* `PUT /vendors/27cc67093475061e3d95369d.json` will update the vendor from the parameters passed.

```json
{
  "name": "Small Media Co."
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the vendor in the response body. If the user does not have access to update the vendor, you'll see `403 Forbidden`. See the **Get vendor** endpoint for more info.


Delete vendor
-------------

* `DELETE /vendors/27cc67093475061e3d95369d.json` will delete the vendor specified and return `204 No Content` if that was successful. If the user does not have access to delete the vendor, you'll see `403 Forbidden`.
