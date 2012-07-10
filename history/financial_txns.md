Financial Transactions
======================

> ** quote **
>
> -Source

Your company's financial history is an immutable reality (or should be!) that is currently pulled from your financial system. A minority of ActiveCell customers have expressed a desire to be able to edit their financial history within the application, but the overwhelming majority prefer to have the facts come from the accounting system, and facts are facts. We agree.

The financial transaction list is detailed record of individual transaction line items pulled from a financial system or imported through the API. Given the sheer volume of transactions possible and the size of each transaction, it is recommended that the aggregated financial summary be employed wherever possible and that the transaction history be filtered as granularly as possible when employed. Most transactions will not have all dimensions populated, and so blank (or "null") values are to be expected for some of these dimensions in each record supplied. Dollar values are expressed as integers in cents, so be certain to convert to dollars by dividing by 100.


Query parameters
----------------
* pd [String] A system-defined BSON ObjectId identifier for the period
* a [String] A system-defined BSON ObjectId identifier for the account
* pt [String] A system-defined BSON ObjectId identifier for the product
* c [String] A system-defined BSON ObjectId identifier for the customer
* e [String] A system-defined BSON ObjectId identifier for the employee
* v [String] A system-defined BSON ObjectId identifier for the vendor


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the financial transaction
* period_id [String] A system-defined BSON ObjectId identifier for the period
* account_id [String] A system-defined BSON ObjectId identifier for the account
* product_id [String] A system-defined BSON ObjectId identifier for the product
* customer_id [String] A system-defined BSON ObjectId identifier for the customer
* employee_id [String] A system-defined BSON ObjectId identifier for the employee
* vendor_id [String] A system-defined BSON ObjectId identifier for the vendor
* document_type [String] A system-defined description of the source document
* document_id [String] A unique document ID provided by the source system (may contain alpha-numeric characters)
* document_line [String] A unique ID to identify the document line (may contain alpha-numeric characters)
* transaction_date [Date] The transaction date of record for the transaction
* amount_cents [Integer] The line amount, in USD converted to cents (divided by 100)


Get financial summary
---------------------

* `GET /financial_summary.json?pd=17cc67093475061e3d95369d&a=27cc67093475061e3d95369d&pt=37cc67093475061e3d95369d&c=47cc67093475061e3d95369d&e=57cc67093475061e3d95369d&v=67cc67093475061e3d95369d` will return a detailed record of financial transaction line items filtered by the query parameters.

```json
[
  [
    "17cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "77cc67093475061e3d95369d",
    "Quickbooks Desktop Invoice",
    "100a",
    "3b",
    "2012-01-01",
    10000
  ],
  [
    "87cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "77cc67093475061e3d95369d",
    "Quickbooks Desktop Bill Payment",
    "129300",
    "1",
    "2012-01-01",
    25000
  ],
  [
    "97cc67093475061e3d95369d",
    "27cc67093475061e3d95369d",
    "37cc67093475061e3d95369d",
    "47cc67093475061e3d95369d",
    "57cc67093475061e3d95369d",
    "67cc67093475061e3d95369d",
    "77cc67093475061e3d95369d",
    "Quickbooks Desktop Journal Entry",
    "100234a",
    "2",
    "2012-01-01",
    10000000
  ]
]
```

**Critical JSON Array note:** Due to the potential size of these datasets, data is transmitted as a JSON Array rather than the traditional "Verbose" JSON featured throughout most of the API. The order of the fields reflects the order in the "Fields" section of this document.

