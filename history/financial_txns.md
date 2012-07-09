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

Note for Aleksey: Does it make sense to consider sending Array JSON vs Verbose JSON for potentially large feeds like this? Let's discuss...

Get financial summary
---------------------

* `GET /financial_summary.json?pd=17cc67093475061e3d95369d&a=27cc67093475061e3d95369d&pt=37cc67093475061e3d95369d&c=47cc67093475061e3d95369d&e=57cc67093475061e3d95369d&v=67cc67093475061e3d95369d` will return a detailed record of financial transaction line items filtered by the query parameters.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "period_id": "27cc67093475061e3d95369d",
    "account_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "vendor_id": "77cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Invoice",
    "document_id": "100a",
    "document_line": "3b",
    "transaction_date": "2012-01-01",
    "amount_cents": 10000
  },
  {
    "id": "87cc67093475061e3d95369d",
    "period_id": "27cc67093475061e3d95369d",
    "account_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "vendor_id": "77cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Bill Payment",
    "document_id": "129300",
    "document_line": "1",
    "transaction_date": "2012-01-01",
    "amount_cents": 25000
  },
  {
    "id": "97cc67093475061e3d95369d",
    "period_id": "27cc67093475061e3d95369d",
    "account_id": "37cc67093475061e3d95369d",
    "product_id": "47cc67093475061e3d95369d",
    "customer_id": "57cc67093475061e3d95369d",
    "employee_id": "67cc67093475061e3d95369d",
    "vendor_id": "77cc67093475061e3d95369d",
    "document_type": "Quickbooks Desktop Journal Entry",
    "document_id": "100234a",
    "document_line": "2",
    "transaction_date": "2012-01-01",
    "amount_cents": 10000000
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

