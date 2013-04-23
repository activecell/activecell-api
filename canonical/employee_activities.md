Employee activities
===================

> **I found that there were these incredibly great people at doing certain things, and you couldn't replace one of these people with 50 average people. They could just do stuff that no number of average people could do.**
>
> -Steve Jobs

In order to figure out how well your employees are doing, it can be very helpful to track or estimate how much time each spends on a range of different activities, from billable client work (in some business models), to Sales, Marketing, Research & Development...filling out TPS reports...tracking time bureaucratically...you name it. Of course, the best situation is where time tracking is automated, or where simplifying assumptions can be used to map employee time to activities. 

This is our canonical list of employee activities, since there often isn't a clean list in a business's financial systems. By mapping employee time to this list, you can gain much in analyzing your employees time in Activecell.

Fields
------

* id [String] A system-defined BSON ObjectId identifier for the employee activity
* name [String] The name of the employee activity


Get employee activities
------------

* `GET /employee_activities.json` will return our canonical list of employee activities. There is no pagination because we curate the list and keep in short.

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

* `GET /employee_activities/17cc67093475061e3d95369d.json` will return the specified employee activity

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Sales"
}
```