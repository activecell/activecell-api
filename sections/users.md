Users
=====

>  I fight for the users. 
> -- <cite>- Tron</cite>

ActiveCell API access is authenticated to a specific user, and that user can view user details for any company to which he/she has access. The processes of creating users and inviting new users to existing companies, however, is built into the companies model. See the **Create company* endpoint for more info.

Get users
------------

* `GET /users.json` will return the all the users for the company. There is no pagination because we currently limit companies to 50 users.

```json
[
  {
    "id": 1,
    "name": "Don Draper",
		"email": "don.draper@sterlingcooper.com"
  },
  {
    "id": 2,
    "name": "Roger Sterling",
		"email": "roger.sterling@sterlingcooper.com"
  },
  {
    "id": 3,
    "name": "Bert Cooper",
		"email": "bert.cooper@sterlingcooper.com"
  }
]
```

Get user
-----------

* `GET /users/1.json` will return the specified user

```json
{
  "id": 1,
  "name": "Don Draper",
	"email": "don.draper@sterlingcooper.com"
}
```


Create user
--------------

* `POST /users.json` will create a new user from the parameters passed.

```json
{
  "name": "Peggy Olson",
  "email": "peggy.olson@sterlingcooper.com"
}
```

* To invite an existing user, simply pass the existing user's id.
* To invite a new user to be associated with the company, provide the name and email, and an email will be sent to the email provided with a password create request
* If the email provided corresponds to an existing user, the user will be added to the company without a password create request

This will return `201 Created`, with the location of the new user in the `Location` header along with the current JSON representation of the user if the creation was a success. See the **Get user* endpoint for more info.


Update user
--------------

* `PUT /users/2.json` will update the user from the parameters passed.

```json
{
  "name": "Roger Sterling",,
	"email": "roger.t.sterling@sterlingcooper.com"
}
```

This will return `200 OK` if the update was a success, along with the current JSON representation of the user in the response body. If the user does not have access to update the user, you'll see `403 Forbidden`. See the **Get user** endpoint for more info.


Delete user
-------------

* `DELETE /users/1.json` will delete the user specified and return `204 No Content` if that was successful. If the user does not have access to delete the user, you'll see `403 Forbidden`.
