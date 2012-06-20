Companies
========

> **What's worth doing is worth doing for money.**
>
> -Wall Street

The company is what ties together all the information in ActiveCell. In the future, reporting will be possible across multiple companies so that franchises can view performance of separate business or for business owners who store separate business units in separate QuickBooks files.

But for today, all reporting flows down from a given company, and the creation of a new user is tied to the creation of a new company. Further, new users can be invited to an existing company by any user who has access to the company.


Fields
------

* id [String] A BSON ObjectId Datatype identifier for the channel (system-defined)
* name [String] The name of the company (user-defined or retrieved from QuickBooks)
* subdomain [String] The subdomain to activecell.com used to access the company's data through the API and analysis through the application
* country-id [String] A BSON ObjectId Datatype identifier for the company's origin country
* postal-code [String] A postal code used in concert with the country field for demographic purposes ("zip code" in the USA)
* url [String] A link to the company's primary website
* industry-id [String] A BSON ObjectId Datatype identifier for the company's industry


Get companies
------------

* `GET /companies.json` will return the all the companies to which the authenticated user has access. There is no pagination because we currently limit users to 50 companies (most users have 1!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Sterling Cooper",
    "subdomain": "sterlingcooper",
    "country-id": "27cc67093475061e3d95369d",
    "postal-code": "10010",
    "url": "sterlingcooper.com",
    "industry-id": "37cc67093475061e3d95369d"
  },
  {
    "id": "47cc67093475061e3d95369d",
    "name": "Sterling Cooper Draper Pryce",
    "subdomain": "scdp",
    "country-id": "27cc67093475061e3d95369d",
    "postal-code": "10010",
    "url": "sterlingcooperdraperpryce.com",
    "industry-id": "37cc67093475061e3d95369d"
  }
]
```

Get company
-----------

* `GET /companies/17cc67093475061e3d95369d.json` will return the specified company and its users

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Sterling Cooper",
  "subdomain": "sterlingcooper",
  "country-id": "27cc67093475061e3d95369d",
  "postal-code": "10010",
  "url": "sterlingcooper.com",
  "industry-id": "37cc67093475061e3d95369d"
  "users": [
    {"id": "57cc67093475061e3d95369d", "name": "Don Draper", "email": "don.draper@sterlingcooper.com"},
    {"id": "67cc67093475061e3d95369d", "name": "Roger Sterling", "email": "roger.sterling@sterlingcooper.com"},
    {"id": "77cc67093475061e3d95369d", "name": "Bert Cooper", "email": "bert.cooper@sterlingcooper.com"}
  ],
}
```


Create company
--------------

* `POST /companies.json` will create a new company and its users (at least one) from the parameters passed.

_Note: In the absence of a company-specific subdomain, requests may be made to app.activecell.com_

```json
{
  "name": "Sterling Cooper Draper Pryce",
  "subdomain": "scdp",
	"country-id": "27cc67093475061e3d95369d",
	"postal-code": "10010",
	"url": "sterlingcooperdraperpryce.com",
	"industry-id": "37cc67093475061e3d95369d"
	"users": [
		{"id": "67cc67093475061e3d95369d"},
	  {"name": "Don Draper", "email": "don.draper@sterlingcooper.com", "password": "reallyWhitman"},
		{"name": "Peggy Olson", "email": "peggy.olson@sterlingcooper.com"}
	]
}
```

* To create a new company associated with an existing user, simply pass the existing user's id in the users array. 
* To create a new user to be associated with the company, provide the name, email, and password for the new user
* If a password is not provided, an email will be sent to the email provided with a password create request

This will return `201 Created`, with the location of the new company in the `Location` header along with the current JSON representation of the company if the creation was a success. See the **Get company* endpoint for more info.


Update channel
--------------

* `PUT /companies/47cc67093475061e3d95369d.json` will update the company from the parameters passed.

```json
{
  "name": "Sterling Cooper Draper Pryce",
  "subdomain": "scdp",
  "country-id": "27cc67093475061e3d95369d",
  "postal-code": "10010",
  "url": "sterlingcooperdraperpryce.com",
  "industry-id": "37cc67093475061e3d95369d"
}
```

_Note: Company users cannot be updated via a PUT request. To add or remove users for an existing company, see the **users** endpoints._

This will return `200 OK` if the update was a success, along with the current JSON representation of the company in the response body. If the user does not have access to update the company, you'll see `403 Forbidden`. See the **Get company** endpoint for more info.


Delete company
-------------

* `DELETE /companies/17cc67093475061e3d95369d.json` will delete the company specified and return `204 No Content` if that was successful. If the user does not have access to delete the company, you'll see `403 Forbidden`.
