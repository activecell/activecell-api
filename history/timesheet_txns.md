Timesheet Transactions
======================

> ** quote **
>
> -Source

Your company's timesheet history may be either:

1. Output from an actual time tracking system, or 
1. An informal estimate of the amount of time each employee spends on a mix of activities and customers

In either case, the value of the historical data is paramount to evaluating the effectiveness of your investments in human capital.

The timesheet transaction list is detailed record of individual transaction line items pulled from a timesheet system or imported through the API. Given the sheer volume of transactions possible and the size of each transaction, it is recommended that the aggregated timesheet summary be employed wherever possible and that the transaction history be filtered as granularly as possible when employed. Most transactions will not have all dimensions populated, and so blank (or "null") values are to be expected for some of these dimensions in each record supplied. Time is expressed simply in minutes. Where the source data has provided hours, these figures have been multiplied by 60.


Query parameters
----------------
* pd [String] A system-defined BSON ObjectId identifier for the period
* a [String] A system-defined BSON ObjectId identifier for the employee activity
* pt [String] A system-defined BSON ObjectId identifier for the product
* c [String] A system-defined BSON ObjectId identifier for the customer
* e [String] A system-defined BSON ObjectId identifier for the employee


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the timesheet transaction
* period_id [String] A system-defined BSON ObjectId identifier for the period
* employee\_activity_id [String] A system-defined BSON ObjectId identifier for the activity
* product_id [String] A system-defined BSON ObjectId identifier for the product
* customer_id [String] A system-defined BSON ObjectId identifier for the customer
* employee_id [String] A system-defined BSON ObjectId identifier for the employee
* document_type [String] A system-defined description of the source document
* document_id [String] A unique document ID provided by the source system (may contain alpha-numeric characters)
* document_line [String] A unique ID to identify the document line (may contain alpha-numeric characters)
* transaction_date [Date] The transaction date of record for the transaction
* amount_minutes [Integer] The aggregated amount, in minutes

Note for Aleksey: Does it make sense to consider sending Array JSON vs Verbose JSON for potentially large feeds like this? Let's discuss...

Get financial summary
---------------------

* `GET /financial_summary.json?pd=17cc67093475061e3d95369d&a=27cc67093475061e3d95369d&pt=37cc67093475061e3d95369d&c=47cc67093475061e3d95369d&e=57cc67093475061e3d95369d` will return a detailed record of financial transaction line items filtered by the query parameters.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "period_id": "27cc67093475061e3d95369d",
    "employee\_activity_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Timesheet",
    "document_id": "100a",
    "document_line": "3b",
    "transaction_date": "2012-01-01",
    "amount_minutes": 120
  },
  {
    "id": "87cc67093475061e3d95369d",
    "period_id": "27cc67093475061e3d95369d",
    "employee\_activity_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Timesheet",
    "document_id": "129300",
    "document_line": "1",
    "transaction_date": "2012-01-01",
    "amount_minutes": 240
  },
  {
    "id": "97cc67093475061e3d95369d",
    "employee\_activity_id": "27cc67093475061e3d95369d",
    "account_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Timesheet",
    "document_id": "100234a",
    "document_line": "2",
    "transaction_date": "2012-01-01",
    "amount_minutes": 480
  }
]
```

Aleksey: Alternatively, we could send and receive Array JSON:

```json
[
  [
    "17cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "Quickbooks Desktop Timesheet",
    "100a",
    "3b",
    "2012-01-01",
    120
  ],
  [
    "87cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "Quickbooks Desktop Timesheet",
    "129300",
    "1",
    "2012-01-01",
    240
  ],
  [
    "97cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "Quickbooks Desktop Timesheet",
    "100234a",
    "2",
    "2012-01-01",
    480
  ]
]
```

