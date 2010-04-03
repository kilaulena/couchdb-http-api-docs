# Security

## Intro

userDoc = users_db.save(CouchDB.prepareUserDoc({name: "Gaius Baltar", roles: ["president"]}, "secretpass"));


## .login()

### .login("username", "password")

### Description:
Does a POST on "_session" with the user details.

### Results
A created [session] (/session) with the user name and roles.

### Returns:
{name: "username", ok: true, roles: ["president"]}

### Prerequisites:
A user doc [prepareUserDoc] (/prepareUserDoc), saved in an [authentication db] (/Security).


## .logout()

### .logout()

### Description:
Does a DELETE on "_session".

### Results
The [session] (/session) where the user name is null.

### Returns:
{ok: true}

### Prerequisites:
A user [session] (/session), as created by [login] (/login).




# Server


# Database


# Documents


# Design Docs

