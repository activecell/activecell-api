Scenarios
=========

> **Worst case scenario? When he wakes up, his mind is completely gone.**
>
> -Inception

ActiveCell allows for multiple "scenarios" for your forecasts. By default, all forecast inputs begin in an initial "Base" scenario, but new scenarios can be created by duplicating an existing scenario and then editing the new scenario.

Note: Historical data is not associated with a scenario. (There should only be one version of what already happened!)


Fields
------

* id [String] A system-defined BSON ObjectId identifier for the scenario
* name [String] The name of the scenario (user-defined, though "Base" is the default first scenario)


Get scenarios
------------

* `GET /scenarios.json` will return the all the scenarios for the company. There is no pagination because we currently limit companies to 10 scenarios (more than 3 is rare!).

```json
[
  {
    "id": "17cc67093475061e3d95369d",
    "name": "Base"
  },
  {
    "id": "27cc67093475061e3d95369d",
    "name": "Optimistic"
  },
  {
    "id": "37cc67093475061e3d95369d",
    "name": "Pessimistic"
  }
]
```


Get scenario
-----------

* `GET /scenarios/17cc67093475061e3d95369d.json` will return the specified scenario and all of its forecast inputs

```json
{
  "id": "17cc67093475061e3d95369d",
  "name": "Base",
	"unit revenue forecast":[
		_See the **Get unit revenue forecast* endpoint for more info_
	],
	"unit cac forecast":[
		_See the **Get unit cac forecast* endpoint for more info_
	],
	"conversion forecast":[
		_See the **Get conversion forecast* endpoint for more info_
	],
	"churn forecast":[
		_See the **Get churn forecast* endpoint for more info_
	],
	"staffing forecast":[
		_See the **Get staffing forecast* endpoint for more info_
	],
	"employee cost forecast":[
		_See the **Get employee cost forecast* endpoint for more info_
	],
	"vendor cost forecast":[
		_See the **Get vendor cost forecast* endpoint for more info_
	]
}
```


Create scenario
--------------

* `POST /scenarios.json` will create a new scenario from the parameters passed.

```json
{
  "name": "Growth mode",
	"unit revenue forecast":[
		_See the **Update unit revenue forecast* endpoint for more info_
	],
	"unit cac forecast":[
		_See the **Update unit cac forecast* endpoint for more info_
	],
	"conversion forecast":[
		_See the **Update conversion forecast* endpoint for more info_
	],
	"churn forecast":[
		_See the **Update churn forecast* endpoint for more info_
	],
	"staffing forecast":[
		_See the **Update staffing forecast* endpoint for more info_
	],
	"employee cost forecast":[
		_See the **Update employee cost forecast* endpoint for more info_
	],
	"vendor cost forecast":[
		_See the **Update vendor cost forecast* endpoint for more info_
	]
}
```

* Alternatively, `POST /scenarios.json` with a "source scenario id" parameter will simply duplicate an existing scenario, returning the new scenario.

```json
{
  "source scenario id": "17cc67093475061e3d95369d",
  "name":"Growth mode"
}
```

This will return `201 Created`, with the location of the new scenario in the `Location` header along with the current JSON representation of the scenario if the creation was a success. See the **Get scenario* endpoint for more info.


Update scenario
--------------

* `PUT /scenarios/27cc67093475061e3d95369d.json` will update the scenario from the parameters passed.

```json
{
  "name": "Exceptional growth mode"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the scenario in the response body. If the user does not have access to update the scenario, you'll see `403 Forbidden`. See the **Get scenario** endpoint for more info.


Delete scenario
-------------

* `DELETE /scenarios/17cc67093475061e3d95369d.json` will delete the scenario specified and return `204 No Content` if that was successful. If the user does not have access to delete the scenario, you'll see `403 Forbidden`.

Note: At least one scenario must exist for a company, so an attempt to delete the last remaining scenario will return `403 Forbidden` as well.