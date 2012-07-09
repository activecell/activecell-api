API documentation for ActiveCell
================================

You can use this site to understand how to connect to the ActiveCell API. We use it ourselves, as a matter of fact, not only for our pet projects and to load up sample data...but indeed our application itself uses the API exclusively to retrieve and persist data. It's called dog-fooding, and we're all over it.

_Editor's note on **API documentation format**:_ This API documentation site draws heavily if not completely from [37signals API documentation](https://github.com/37signals/api). We feel they really got it right and that others should get their API documentation into such a simple and digestible format. Hat's off to the crew at 37signals. Thanks for the inspiration!

_Editor's note on **Sample Data**:_ Our sample data is pulled from AMC's tv show [Mad Men](http://en.wikipedia.org/wiki/Mad_Men). Some company names and user names and various other ideas are drawn from the plots of this show but aren't intended to reflect any actual business transactions or relationships. It's just sample data!

Making a request
----------------

All URLs start with `https://[subdomain].activecell.com/api/v1/`. **SSL only**. The path is prefixed with the account id and the API version. If we change the API in backward-incompatible ways, we'll bump the version marker and maintain stable support for the old URLs.

To make a request for all the channels for your company, you would append the channels index path to the base url. If your company domain was "sterlingcooper" you would form something like https://sterlingcooper.activecell.com/api/v1/channels.json. In curl, that looks like:

```shell
curl -u user:pass -H 'User-Agent: MyApp (don.draper@sterlingcooper.com)' https://sterlingcooper.activecell.com/api/v1/channels.json
```

To create something, it's the same deal except you also have to include the `Content-Type` header and the JSON data:

```shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (don.draper@sterlingcooper.com)' \
  -d '{ "name": "My new channel!" }' \
  https://sterlingcooper.activecell.com/api/v1/channels.json
```

That's all!


Authentication
--------------

If you're making a private integration with ActiveCell for your own purposes, you can use HTTP Basic authentication. This is secure since all requests use SSL.

_Future: If you're making a public integration with ActiveCell for others to enjoy, you must use OAuth 2. This allows users to authorize your application to use ActiveCell on their behalf without having to copy/paste API tokens or touch sensitive login info._


No XML, just JSON
-----------------

We only support JSON for serialization of data. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into ActiveCell. **All API URLs end in .json to indicate that they accept and return JSON.**

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the `Content-Type` header.

Use HTTP caching
----------------

You must make use of the HTTP freshness headers to lessen the load on our servers (and increase the speed of your application!). Most requests we return will include an `ETag` or `Last-Modified` header. When you first request a resource, store this value, and then submit them back to us on subsequent requests as `If-None-Match` and `If-Modified-Since`. If the resource hasn't changed, you'll see a `304 Not Modified` response, which saves you the time and bandwidth of sending something you already have.


Handling errors
---------------

If ActiveCell is having trouble, you might see a 5xx error. `500` means that the app is entirely down, but you might also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later. 

We have another API for checking our system status at http://status.activecell.com/api.


Rate limiting
-------------

You can perform up to 500 requests per 10 second period from the same IP address for the same account. If you exceed this limit, you'll get a [429 Too Many Requests](http://tools.ietf.org/html/draft-nottingham-http-new-status-02#section-4) response for subsequent requests. Check the `Retry-After` header to see how many seconds to wait before retrying the request.



API ready for use
-----------------

Canonical data (get only):

* [Periods](https://github.com/profitably/activecell-api/blob/master/canonical/periods.md)
* [Industries](https://github.com/profitably/activecell-api/blob/master/canonical/industries.md)
* [Countries](https://github.com/profitably/activecell-api/blob/master/canonical/countries.md)
* [Employee activities](https://github.com/profitably/activecell-api/blob/master/canonical/employee_activities.md)

Company data:

* [Users](https://github.com/profitably/activecell-api/blob/master/company/users.md)
* [Companies](https://github.com/profitably/activecell-api/blob/master/company/companies.md)
* [Scenarios](https://github.com/profitably/activecell-api/blob/master/company/scenarios.md)
* [Accounts](https://github.com/profitably/activecell-api/blob/master/company/accounts.md)

Product data:

* [Products](https://github.com/profitably/activecell-api/blob/master/product/products.md)
* [Revenue streams](https://github.com/profitably/activecell-api/blob/master/product/streams.md)

Customer data:

* [Customers](https://github.com/profitably/activecell-api/blob/master/customer/customers.md)
* [Segments](https://github.com/profitably/activecell-api/blob/master/customer/segments.md)
* [Channels (including segment mix)](https://github.com/profitably/activecell-api/blob/master/customer/channels.md)
* [Customer acquisition stages](https://github.com/profitably/activecell-api/blob/master/customer/stages.md)

Employee data:

* [Employees](https://github.com/profitably/activecell-api/blob/master/employee/employees.md)
* [Employee types (including activity mix)](https://github.com/profitably/activecell-api/blob/master/employee/employee_types.md)

Vendor data:

* [Vendors](https://github.com/profitably/activecell-api/blob/master/vendor/vendors.md)
* [Categories](https://github.com/profitably/activecell-api/blob/master/vendor/categories.md)

History:

* [Conversion summary](https://github.com/profitably/activecell-api/blob/master/history/conversion_summary.md)
* [Financial summary](https://github.com/profitably/activecell-api/blob/master/history/financial_summary.md)
* [Financial transactions](https://github.com/profitably/activecell-api/blob/master/history/financial_txns.md)
* [Timesheet summary](https://github.com/profitably/activecell-api/blob/master/history/timesheet_summary.md)
* [Timesheet transactions](https://github.com/profitably/activecell-api/blob/master/history/timesheet_txns.md)
* [Raw document](https://github.com/profitably/activecell-api/blob/master/history/document.md)

Forecasts:

* [Unit revenue forecast]()
* [Unit cac forecast]()
* [Conversion forecast]()
* [Churn forecast]()
* [Staffing forecast]()
* [Employee cost forecast]()
* [Vendor cost forecast]()


Help us make it better
----------------------

Please tell us how we can make the API better. If you have a specific feature request or if you found a bug, please use GitHub issues. Fork these docs and send a pull request with improvements.
