# Database

## Database Intro
A new db is specified like this:
    db = new CouchDB("spec_db", {"X-Couch-Full-Commit":"false"});
It then has to be [created](/createDb) before you can do anything with it.


## .request()

### db.request(method, uri, requestOptions)

### Description
Combines the headers of the [db](/database-intro) with the requestOptions and passes the parameters to [CouchDB.request](/request), which creates a [new XMLHTTPRequest](/newXhr).

### Results
The XMLHTTPRequest has been sent with the given parameters and the headers options of the db.

### Returns
A new XMLHTTPRequest with readyState 4 as made by [CouchDB.request](/request).

### Example
     db.request("GET", "/test_db")
    
    
    

## .createDb()

### db.createDb()

### Description
Creates the db.
  
### Results
The db is created, with update sequence 0.

### Returns
{"ok" : true}


## .deleteDb()

### db.deleteDb()

### Description
Deletes the db.
  
### Results
The db is deleted.

### Returns
{"ok" : true}

