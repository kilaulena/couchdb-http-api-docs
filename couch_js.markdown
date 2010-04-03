# Security

## Intro

userDoc = users_db.save(CouchDB.prepareUserDoc({name: "Gaius Baltar", roles: ["president"]}, "secretpass"));


## .login()

### .login("username", "password")

### Returns:
{name: "username", ok: true, roles: ["president"]}

### Prerequisites:
A user doc [prepareUserDoc] (/prepareUserDoc), saved in an [authentication db] (/Security).

### Description:
Does a POST on "_session" with the user details. Results in a created [session] (/session).



# Server


# Database


# Documents


# Design Docs

