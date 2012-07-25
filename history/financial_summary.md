Financial Summary
=================

> ** quote **
>
> -Source

Your company's financial history is an immutable reality (or should be!) that is currently pulled from your financial system. A minority of ActiveCell customers have expressed a desire to be able to edit their financial history within the application, but the overwhelming majority prefer to have the facts come from the accounting system, and facts are facts. We agree.

The financial summary is an aggregate of all the individual transactions that occur for a given period, account, product, customer, employee, and vendor. Most transactions will not have all dimensions populated, and so blank (or "null") values are to be expected for some of these dimensions in each record supplied. Dollar values are expressed as integers in cents, so be certain to convert to dollars by dividing by 100.


Fields (order of fields is prescriptive for JSON Array)
-------------------------------------------------------

* period_id [String] A system-defined BSON ObjectId identifier for the period
* account_id [String] A system-defined BSON ObjectId identifier for the account
* product_id [String] A system-defined BSON ObjectId identifier for the product
* customer_id [String] A system-defined BSON ObjectId identifier for the customer
* employee_id [String] A system-defined BSON ObjectId identifier for the employee
* vendor_id [String] A system-defined BSON ObjectId identifier for the vendor
* amount_cents [Integer] The aggregated amount, in USD converted to cents (divided by 100)


Get financial summary
---------------------

* `GET /financial_summary.json` will return an aggregated summary of financial transactions for the company in the application's date range scope.

```json
[
  {
    "period_id": "27cc67093475061e3d95369d",
    "account_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "vendor_id": "17cc67093475061e3d95369d",
    "amount_cents": 10000
  },
  {
    "period_id": "600d3c64b0207ae648000005",
    "account_id": "700d3c64b0207ae648000005",
    "product_id": "800d3c64b0207ae648000005",
    "customer_id": "900d3c64b0207ae648000005",
    "employee_id": "100d3c64b0207ae648000005",
    "vendor_id": "200d3c64b0207ae648000005",
    "amount_cents": 20000
  },
  {
    "period_id": "267d3c64b0313ae648909021",
    "account_id": "367d3c64b0313ae648909021",
    "product_id": "467d3c64b0313ae648909021",
    "customer_id": "567d3c64b0313ae648909021",
    "employee_id": "667d3c64b0313ae648909021",
    "vendor_id": "767d3c64b0313ae648909021",
    "amount_cents": 30000    
  }
]
```
