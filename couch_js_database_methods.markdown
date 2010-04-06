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


## .ensureFullCommit()

### db.ensureFullCommit()

### Description
Does a POST request to the db and "_ensure_full_commit"
  
### Results
Tells the db to do an fsync (write data to disk immediately).

### Returns
    {"ok" : true} 
and the start time of the db instance.


## .query()

### db.query(mapFun, reduceFun, options, keys, language)

### Description
Applies the mandatory map function and the optional reduce function to the contents of database and returns the results. 
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).
The result can be specified more by querying only for single keys.
The language of the query has to be specified when another language than the default JavaScript is used. [Erlang views have to be enabled](/http://wiki.apache.org/couchdb/EnableErlangViews) beforehand.

### Returns
The total number of rows and an array of rows, each row containing one result of the query.

### Example
     db.query("function(doc) { emit(doc._id, null); }", null, {"include_docs":"true"}, ["123", "456"])


## .view()

### db.view(viewname, options, keys)

### Description
Applies the view to the contents of database and returns the results. When there are no keys given, it does a GET request to the view path with the options as params, or a POST request with the keys as body.
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).
The result can be specified more by querying only for single keys.

### Returns
The total number of rows and an array of rows, each row containing one result of the query, or null when the view doesn't exist.

### Example
    db.view('spec_db/viewname', {"include_docs":"true"}, ["456"])


## .info()

### db.info()

### Description
Does a GET request to the db. 

### Returns
db_name, doc_count, doc_del_count, update_seq, purge_seq, compact_running, disk_size, instance_start_time, disk_format_version


## .allDocs()

### db.allDocs(options, keys)

### Description
When there are no keys given, it does a GET request to "_all_docs" with the options as params, or a POST request with the keys as body.
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).
The result can be specified more by querying only for single keys.

### Returns
The total number of rows and an array of rows, each row containing one result of the query.

### Example
    db.allDocs({"include_docs":"true"}, ["456"])


## .changes()

### db.changes(options)

### Description
Does a GET request to "_changes" with the options as params.
Options can include the [Changes Options of the HTTP database API](http://wiki.apache.org/couchdb/HTTP_database_API#Changes).

### Returns
The last sequence and an array with results. Each result contains the ID and sequence of the changed document and an array with all the changes. For each change the revision is specified.

### Example
    db.changes({"since":"1"})
    
    

## .compact()

### db.compact()

### Description
Does a POST request to the db and "_compact". Compacts the db.

### Returns
    {"ok" : true}
    

## .viewCleanup()

### db.viewCleanup()

### Description
Does a POST request to the db and "_view_cleanup". Cleans old view output from disk. 

### Returns
    {"ok" : true}
    
    

## .setDbProperty()

### db.setDbProperty(propId, propValue)

### Description
Does a PUT request to the db and the propId with the propValue as body.
  
### Results
The db property is set to the specified value.

### Returns
    {"ok" : true}
    
### Example
    db.setDbProperty("_revs_limit", 1500)
    
    

## .getDbProperty()

### db.getDbProperty(propId)

### Description
Does a GET request to the db and the propId.
  
### Returns
The property value.
    
### Example
    db.getDbProperty("_revs_limit")
    
    

## .setSecObj()

### db.setSecObj(secObj)

### Description
Does a PUT request to the db and "_security" with the security object as body.
  
### Results
The security object is set to the specified value.

### Returns
    {"ok" : true}
    
### Example
    db.setSecObj({"admins" : {"names" : ["laura"], "roles" : ["boss"]}})
    

## .getSecObj()

### db.getSecObj(propId)

### Description
Does a GET request to the db and "_security".
  
### Returns
The security object.

    
    
