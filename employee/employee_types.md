Employee types
==============

> **I realize that I'm the president of this company, the man that's responsible for everything that goes on here.  
> So, I want to state, right now, that anything that happened is not my fault.**
>
> -How to Succeed in Business Without Really Trying

In most business with fewer than 100 employees, there are typically only a handful of different job roles in a company, and in some cases, lots of people are wearing lots of different hats. But when and where you can isolate a series of employees playing the same role, it can be very useful to look at compensation and performance for that role, specifically.

Further, the vast majority of staffing plans are built at the job role or employee type level of granularity. You plan for the number of salespeople you will need, the number of billable resources you will need, or the number of builders.

Fields
------

* id [String] A system-defined BSON ObjectId identifier for the employee type
* name [String] The name of the employee type (user-defined or imported from QuickBooks)


Get employee types
------------

* `GET /employee_types.json` will return the all the employee types for the company. There is no pagination because we currently limit companies to 50 employee types (more than 10 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Partner"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Creative"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Account Executive"
  }
]
```


Get employee type
-----------

* `GET /employee_types/17cc67093475061e3d95369d.json` will return the specified employee type and its forecast channel/segment mix

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Partner"
}
```


Create employee type
--------------

* `POST /employee_types.json` will create a new employee type from the parameters passed.

```json
{
  "name": "Assistant"
}
```

This will return `201 Created`, with the location of the new employee type in the `Location` header along with the current JSON representation of the employee type if the creation was a success. See the **Get channel* endpoint for more info.


Update employee type
--------------

* `PUT /employee_types/27cc67093475061e3d95369d.json` will update the employee type from the parameters passed.

```json
{
  "name": "Partner"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the employee type in the response body. If the user does not have access to update the employee type, you'll see `403 Forbidden`. See the **Get employee type** endpoint for more info.


Delete employee type
-------------

* `DELETE /employee_types/27cc67093475061e3d95369d.json` will delete the employee type specified and return `204 No Content` if that was successful. If the user does not have access to delete the employee type, you'll see `403 Forbidden`.

Note: At least one employee type must exist for a company, so an attempt to delete the last remaining employee type will return `403 Forbidden` as well.