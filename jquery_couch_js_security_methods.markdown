# Security

## Security Intro

See [couch.js / Security Intro](/security-intro)


## .session()

### $.couch.session(options)

### Description
Does a GET request to "_session". 

### Returns
    {"ok": true, "userCtx": {"name": "username", "roles": ["customrole"]}, "info": {"authentication_db": "_users", "authentication_handlers": ["oauth", "cookie", "default"], "authenticated": "cookie"}}

### Prerequisites
A user [session](/session), as created by [login](/login). When there is no session, userCtx.name is null.



## .userDb(callback)

### $.couch.userDb(callback)

### Description
Creates [a new db](/database-intro) with the name of the [authentication db](/security-intro) and executes the callback function with the db as parameter.



## .signup()

### $.couch.signup(user_doc, password, options)

### Description
* Hashes the password 
* Adds an empty roles array to the user_doc when not specified
* Adds an _id, composed of "org.couchdb.user:" and name, to the user_doc when not specified
* Saves the user_doc with options as parameters in the [userDb](/userDb)
* Performs the success callback on the saved user_doc

### Response
The saved user_doc.

### Results
The user_doc is saved in the [userDb](/userDb).



## .login()

### $.couch.login(options)

### Description
Does a POST request to "_session" with username and password, they have to be present in the options hash.
Throws a 404 error when the password is wrong or there is no user with that username stored in the [userDb](/userDb).

### Results
A created [session](/session) with the user name and roles.

### Returns
    {"ok": true, "name": "username", "roles": ["customrole"]}

### Prerequisites
A [signed up user](/signup), saved in an [authentication db](/security-intro).


## .logout()

### $.couch.logout(options)

### Description
Does a DELETE request to "_session".

### Results
The [session's](/session) user name is set to null and the custom role is removed from the roles array.

### Returns
    {"ok": true}

### Prerequisites
A user [session](/session), as created by [login](/login).
