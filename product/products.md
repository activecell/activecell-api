Products
========

> **I don't even own a gun, let alone many guns that would necessitate an entire rack. 
> What am I gonna do with a gun rack?**
>
> -Wayne's World

Some businesses sell products. Some businesses sell services. Some businesses sell both. For brevity, we refer to the "items" being sold as individual products, even if in reality they are services, and if this is an awkward construction for your business, we will shortly be able to customize the verbiage on the site for your particular business, so hang in there!

Your product list may map to a list in your accounting or inventory software, or it may be more informal, something to track manually using ActiveCell.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the product
* name [String] The name of the product (user-defined or imported from QuickBooks)
* revenue_stream [RevenueStream] Optional: the revenue stream to which the product/service is assigned


Get products
------------

* `GET /products.json` will return the all the products for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Consulting",
    "revenue_stream":{
      "id":"47cc67093475061e3d95369d",
      "name":"Professional services"
    }
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Television ads",
    "revenue_stream":{
      "id":"57cc67093475061e3d95369d",
      "name":"Media purchases"
    }
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Radio ads",
    "revenue_stream":{
      "id":"57cc67093475061e3d95369d",
      "name":"Media purchases"
    }
  }
]
```


Get product
-----------

* `GET /products/17cc67093475061e3d95369d.json` will return the specified product

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Consulting",
  "revenue_stream":{
    "id":"47cc67093475061e3d95369d",
    "name":"Professional services"
  }
}
```


Create product
--------------

* `POST /products.json` will create a new product from the parameters passed.

```json
{
  "name": "Magazine ads",
  "revenue_stream_id":"67cc67093475061e3d95369d"
}
```

This will return `201 Created`, with the location of the new product in the `Location` header along with the current JSON representation of the product if the creation was a success. See the **Get product** endpoint for more info.


Update product
--------------

* `PUT /products/27cc67093475061e3d95369d.json` will update the product from the parameters passed.

```json
{
  "name": "Affiliate revenue",
  "revenue_stream_id": "67cc67093475061e3d95369d"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the product in the response body. If the user does not have access to update the product, you'll see `403 Forbidden`. See the **Get product** endpoint for more info.


Delete product
-------------

* `DELETE /products/27cc67093475061e3d95369d.json` will delete the product specified and return `204 No Content` if that was successful. If the user does not have access to delete the product, you'll see `403 Forbidden`.
