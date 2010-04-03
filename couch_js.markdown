# Security

## Security Intro

The default authentication db is called "_users". In this db the information about the users is stored. You can change the authentication db like this:

    users_db = new CouchDB("custom_users_db");
    users_db.createDb();

    CouchDB.request("PUT", "/_config/couch_httpd_auth/authentication_db", { body: JSON.stringify("custom_users_db")});

You can "signup" like this:

    userDoc = CouchDB.prepareUserDoc({name: "username", roles: ["customrole"]}, "secretpassword");

    users_db.save(userDoc);


## .login()

### CouchDB.login("username", "secretpassword")

### Description
Does a POST on "_session" with the user details.

### Results
A created [session] (/session) with the user name and roles.

### Returns
    {"ok": true, "name": "username", "roles": ["customrole"]}

### Prerequisites
A user doc [prepareUserDoc] (/prepareUserDoc), saved in an [authentication db] (/security-intro).


## .logout()

### CouchDB.logout()

### Description
Does a DELETE on "_session".

### Results
The [session's] (/session) user name is set to null and the custom role is removed from the roles array.

### Returns
    {"ok": true}

### Prerequisites
A user [session] (/session), as created by [login] (/login).


## .session()

### CouchDB.session(options)

### Description
Does a GET on "_session". 

### Returns
    {"ok": true, "userCtx": {"name": "username", "roles": ["customrole"]}, "info": {"authentication_db": "_users", "authentication_handlers": ["oauth", "cookie", "default"], "authenticated": "cookie"}}

### Prerequisites
A user [session] (/session), as created by [login] (/login).


## .prepareUserDoc()

### CouchDB.prepareUserDoc(userDoc, "secretpassword")

### Description
* Hashes the password 
* Adds an empty roles array to the userDoc when not specified
* Adds an _id, composed of user_prefix and name, to the userDoc when not specified

### Returns
    {"name": "username", "roles": ["customrole"], "_id": "org.couchdb.user:customrole", "salt":"a salt", "password_sha": "hashed password", "type":"user"}
    
### Example
    CouchDB.prepareUserDoc({name: "username", roles: ["customrole"]}, "secretpassword")
  
    
# Server

## .allDbs()

### CouchDB.allDbs(options)

### Description
Does a GET on "_all_dbs". 

### Returns
An array with all the databases.



# Database


# Documents


# Design Docs

## .allDesignDocs()

### CouchDB.allDesignDocs()

### Description
Goes through [all dbs] (/allDbs) and returns all [design docs] (/designDocs) for each db.

### Returns
An array with all dbs, for each db the id and revision of every design document.

### Example
When there is one database "test_db" and one design document "mydesign", the result is this:
    {"test_db": {"total_rows": 1, "offset": 0, "rows": [{"id": "_design/spec_db", "key": "_design/mydesign", "value": {"rev": "1-3885802b8f5804e8f03cda99df8e6cc7"}}]}}

