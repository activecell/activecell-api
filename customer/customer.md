Customers
========

> **This job would be great if it weren't for the $&@^#@ customers.**  
> **Which ones?**  
> **All of them.**
>
> -Clerks


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the customer
* name [String] The name of the customer (user-defined or imported from QuickBooks)
* channel [Channel] Optional: the customer channel to which the customer is assigned
* segment [Segment] Optional: the customer segment to which the customer is assigned


Get customers
------------

* `GET /customers.json` will return the all the customers for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Lucky Strike",
    "channel":{
      "id":"47cc67093475061e3d95369d",
      "name":"Content marketing"
    },
    "segment":{
      "id":"57cc67093475061e3d95369d",
      "name":"Platinum"
    }
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "London Fog",
    "channel":{
      "id":"67cc67093475061e3d95369d",
      "name":"Direct sales"
    },
    "segment":{
      "id":"77cc67093475061e3d95369d",
      "name":"Gold"
    }
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Unilever",
    "channel":{
      "id":"87cc67093475061e3d95369d",
      "name":"Events"
    },
    "segment":{
      "id":"97cc67093475061e3d95369d",
      "name":"Silver"
    }
  }
]
```


Get customer
-----------

* `GET /customers/17cc67093475061e3d95369d.json` will return the specified customer

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Lucky Strike",
  "channel":{
    "id":"47cc67093475061e3d95369d",
    "name":"Content marketing"
  },
  "segment":{
    "id":"57cc67093475061e3d95369d",
    "name":"Platinum"
  }
}
```


Create customer
--------------

* `POST /customers.json` will create a new customer from the parameters passed.

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Lucky Strike",
  "channel":{"id":"47cc67093475061e3d95369d"},
  "segment":{"id":"57cc67093475061e3d95369d"}
}
```

This will return `201 Created`, with the location of the new customer in the `Location` header along with the current JSON representation of the customer if the creation was a success. See the **Get customer** endpoint for more info.


Update customer
--------------

* `PUT /customers/27cc67093475061e3d95369d.json` will update the customer from the parameters passed.

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Lucky Strike",
  "channel":{"id":"47cc67093475061e3d95369d"},
  "segment":{"id":"57cc67093475061e3d95369d"}
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the customer in the response body. If the user does not have access to update the customer, you'll see `403 Forbidden`. See the **Get customer** endpoint for more info.


Delete customer
-------------

* `DELETE /customers/27cc67093475061e3d95369d.json` will delete the customer specified and return `204 No Content` if that was successful. If the user does not have access to delete the customer, you'll see `403 Forbidden`.
