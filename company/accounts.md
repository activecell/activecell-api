Scenarios
=========

> **Corporate Accounts Payable, Nina speaking. Just a moment.**
>
> -Office Space

A company's "chart of accounts" is a listing of financial accounts to which transactions are booked during the accounting process. In double-entry bookkeeping, each transaction impacts two account, thus keeping the accounts "in balance."

The accounts are almost always pulled directly from the company's accounting software, where they were either added as defaults, customized by users and accountants, or both.


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the account
* name [String] The name of the account (user-defined)
* type [String] The account type must be one of the canonical types (see below)
* sub_type [String] User-defined sub-classifications below account type
* account_number [String] An optional, user-defined number used for sorting
* parent\_account_id [String] An optional BSON ObjectId identifier for a parent account
* current\_balance [Integer] Current account balance (applies to Asset, Liability, and Equity only)
* current\_balance\_currency [String] A three letter currency code for the current_balance field
* balance\_as\_of [Date] Date for which the current_balance field is valid (close of business)
* is_active [Boolean] A flag to specify if the account is still active

Valid account types: 

* 'Asset'
* 'Liability'
* 'Equity'
* 'Revenue' ('Income' will be overwritten as 'Revenue')
* 'Cost of Goods Sold'
* 'Expense'
* 'Non-Posting'


Get accounts
------------

* `GET /accounts.json` will return the all the accounts for the company.

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Primary Checking Account",
    "type":"Asset",
    "sub_type":"Bank",
    "account_number":"72613",
    "current\_balance":10000000,
    "current\_balance\_currency":"USD",
    "balance\_as\_of":"2012-01-01",
    "is_active":true
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Payroll",
    "type":"Expense",
    "sub_type":"Payroll",
    "account_number":"8237",
    "is_active":true
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Wages and Salaries",
    "type":"Expense",
    "sub_type":"Payroll",
    "account_number":"8237a",
    "parent\_account_id":"27cc67093475061e3d95369d",
    "is_active":true
  }
]
```


Get account
-----------

* `GET /accounts/17cc67093475061e3d95369d.json` will return the specified account and all of its forecast inputs

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Primary Checking Account",
  "type":"Asset",
  "sub_type":"Bank",
  "account_number":"72613",
  "current\_balance":10000000,
  "current\_balance\_currency":"USD",
  "balance\_as\_of":"2012-01-01",
  "is_active":true
}
```


Create account
--------------

* `POST /accounts.json` will create a new account from the parameters passed.

```json
{
  "name": "Primary Checking Account",
  "type":"Asset",
  "sub_type":"Bank",
  "account_number":"72613",
  "current\_balance":10000000,
  "current\_balance\_currency":"USD",
  "balance\_as\_of":"2012-01-01",
  "is_active":true
}
```

This will return `201 Created`, with the location of the new account in the `Location` header along with the current JSON representation of the account if the creation was a success. See the **Get account* endpoint for more info.


Update account
--------------

* `PUT /accounts/27cc67093475061e3d95369d.json` will update the account from the parameters passed.

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Primary Checking Account",
  "type":"Asset",
  "sub_type":"Bank",
  "account_number":"72613",
  "current\_balance":10000000,
  "current\_balance\_currency":"USD",
  "balance\_as\_of":"2012-01-01",
  "is_active":true
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the account in the response body. If the user does not have access to update the account, you'll see `403 Forbidden`. See the **Get account** endpoint for more info.


Delete account
-------------

* `DELETE /accounts/17cc67093475061e3d95369d.json` will delete the account specified and return `204 No Content` if that was successful. If the user does not have access to delete the account, you'll see `403 Forbidden`.