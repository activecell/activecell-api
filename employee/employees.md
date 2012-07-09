Employees
=========

> **Hello Jedediah.  
> Hello, Charlie. I didn't know we were speaking...  
> Sure, we're speaking, Jedediah: you're fired.**
>
> -Citizen Kane

Increasingly, payroll costs outweigh all other expenses a business faces, in some businesses massively. And yet, many businesses struggle to measure performance for their employees in ways similar to other investments. Managers often excuse this, claiming businesses want to build an employee-centric culture and not burden information workers with bureaucratic tracking or specific performance targets.

But if you automate tracking and make it painless, the fruit that can be yielded from smart employee-level analysis can really drive a business forward, identify and reward high-performers, and identify under-performers for corrective measure.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the employee
* name [String] The name of the employee (user-defined or imported from QuickBooks)
* employee_type [EmployeeType] The employee type to which the employee is assigned


Get employees
------------

* `GET /employees.json` will return the all the employees for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Roger Sterling",
    "employee_type":{
      "id":"47cc67093475061e3d95369d",
      "name":"Partner"
    }
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Don Draper",
    "employee_type":{
      "id":"57cc67093475061e3d95369d",
      "name":"Creative"
    }
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Pete Campbell",
    "employee_type":{
      "id":"57cc67093475061e3d95369d",
      "name":"Account Executive"
    }
  }
]
```


Get employee
-----------

* `GET /employees/17cc67093475061e3d95369d.json` will return the specified employee

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Roger Sterling",
  "employee_type":{
    "id":"47cc67093475061e3d95369d",
    "name":"Partner"
  }
```


Create employee
--------------

* `POST /employees.json` will create a new employee from the parameters passed.

```json
{
  "name": "Roger Sterling"
  "employee_type": {"id":"67cc67093475061e3d95369d"}
}
```

This will return `201 Created`, with the location of the new employee in the `Location` header along with the current JSON representation of the employee if the creation was a success. See the **Get channel* endpoint for more info.


Update employee
--------------

* `PUT /employees/27cc67093475061e3d95369d.json` will update the employee from the parameters passed.

```json
{
  "name": "Roger Sterling"
  "employee_type":{"id":"67cc67093475061e3d95369d"}
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the employee in the response body. If the user does not have access to update the employee, you'll see `403 Forbidden`. See the **Get employee** endpoint for more info.


Delete employee
-------------

* `DELETE /employees/27cc67093475061e3d95369d.json` will delete the employee specified and return `204 No Content` if that was successful. If the user does not have access to delete the employee, you'll see `403 Forbidden`.
