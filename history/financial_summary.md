Financial Summary
=================

> ** quote **
>
> -Source

Your company's financial history is an immutable reality (or should be!) that is currently pulled from your financial system. A minority of ActiveCell customers have expressed a desire to be able to edit their financial history within the application, but the overwhelming majority prefer to have the facts come from the accounting system, and facts are facts. We agree.

The financial summary is an aggregate of all the individual transactions that occur for a given period, account, product, customer, employee, and vendor. Most transactions will not have all dimensions populated, and so blank (or "null") values are to be expected for some of these dimensions in each record supplied. Dollar values are expressed as integers in cents, so be certain to convert to dollars by dividing by 100.


Fields
------

* period_id [String] A system-defined BSON ObjectId identifier for the period
* account_id [String] A system-defined BSON ObjectId identifier for the account
* product_id [String] A system-defined BSON ObjectId identifier for the product
* customer_id [String] A system-defined BSON ObjectId identifier for the customer
* employee_id [String] A system-defined BSON ObjectId identifier for the employee
* vendor_id [String] A system-defined BSON ObjectId identifier for the vendor
* amount_cents [Integer] The aggregated amount, in USD converted to cents (divided by 100)

Note for Aleksey: Does it make sense to consider sending Array JSON vs Verbose JSON for potentially large feeds like this? Let's discuss...

Get financial summary
---------------------

* `GET /financial_summary.json` will return an aggregated summary of financial transactions for the company in the application's date range scope.

```json
[
  {
    "period_id": "17cc67093475061e3d95369d",
    "account_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "vendor_id": "67cc67093475061e3d95369d",
    "amount_cents": 10000
  },
  {
    "period_id": "77cc67093475061e3d95369d",
    "account_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "vendor_id": "67cc67093475061e3d95369d",
    "amount_cents": 20000
  },
  {
    "period_id": "87cc67093475061e3d95369d",
    "account_id": "27cc67093475061e3d95369d",
    "product_id": "37cc67093475061e3d95369d",
    "customer_id": "47cc67093475061e3d95369d",
    "employee_id": "57cc67093475061e3d95369d",
    "vendor_id": "67cc67093475061e3d95369d",
    "amount_cents": 30000
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
    10000
  ],
  [
    "77cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    20000
  ],
  [
    "87cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    30000
  ]
]
```

