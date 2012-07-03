Employee activities
===================

> **  
> **
>
> -

[paragraph 1]

[paragraph 2]

Fields
------

* id [String] A system-defined BSON ObjectId identifier for the employee activity
* name [String] The name of the employee activity


Get employee activities
------------

* `GET /employee-activities.json` will return our canonical list of industries. There is no pagination because we curate the list and keep in short.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Sales"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Marketing"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Billable time"
  }
]
```


Get employee activity
-----------

* `GET /employee-activities/17cc67093475061e3d95369d.json` will return the specified employee activity

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Sales"
}
```