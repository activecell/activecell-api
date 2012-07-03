Expense Categories
==================

> **Spare no expense.**
>
> -Jurassic Park

All of your business expenses naturally fall into categories, most often in sync with expense items in your chart of accounts. For this sort of analysis, however, we exclude payroll costs, which are covered under the employees section. Similarly, many businesses prefer to exclude contractors who act as employees in this section.

By analyzing your spend at the category level, you can quickly identify cost savings opportunities across your vendor base and understand where you are getting the most bang for your buck.

Fields
------

* id [String] A system-defined BSON ObjectId identifier for the category
* name [String] The name of the category (user-defined)


Get categories
------------

* `GET /categories.json` will return the all the categories for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Media buys"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Rent"
  }
]
```


Get category
-----------

* `GET /categories/1.json` will return the specified category

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Media buys"
}
```


Create category
--------------

* `POST /categories.json` will create a new category from the parameters passed.

```json
{
  "name": "Media buys"
}
```

This will return `201 Created`, with the location of the new category in the `Location` header along with the current JSON representation of the category if the creation was a success. See the **Get category* endpoint for more info.


Update category
--------------

* `PUT /categories/27cc67093475061e3d95369d.json` will update the categories from the parameters passed.

```json
{
  "name": "Media buys"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the category in the response body. If the user does not have access to update the category, you'll see `403 Forbidden`. See the **Get category** endpoint for more info.


Delete category
-------------

* `DELETE /categories/17cc67093475061e3d95369d.json` will delete the category specified and return `204 No Content` if that was successful. If the user does not have access to delete the category, you'll see `403 Forbidden`.

Note: At least one category must exist for a company, so an attempt to delete the last remaining category will return `403 Forbidden` as well.