# Database

## Database Intro
A new db is specified like this:
    db = $.couch.db("spec_db");
    
It then has to be [created](/create) before you can do anything with it.


## .compact()

### db.compact(options)

### Description
Does a POST request to the db and "_compact". Compacts the db.

### Response
    {"ok" : true}
    
    
    
## .viewCleanup()

### db.viewCleanup(options)

### Description
Does a POST request to the db and "_view_cleanup". Cleans old view output from disk. 

### Returns
    {"ok" : true}
    
    

## .compactView()

### db.compactView(groupname, options)

### Description
Does a POST request to the db, "_compact" and the groupname. Cleans old output from this view from disk. 
Raises a 404 error when the design doesn't exist.

### Returns
    {"ok" : true}



## .create()

### db.create(options)

### Description
Creates the db.
  
### Results
The db is created, with update sequence 0.

### Response
    {"ok" : true}


## .drop()

### db.drop(options)

### Description
Deletes the db.
  
### Results
The db is deleted.

### Response
    {"ok" : true}
    

## .info()

### db.info(options)

### Description
Does a GET request to the db. 

### Response
db_name, doc_count, doc_del_count, update_seq, purge_seq, compact_running, disk_size, instance_start_time, disk_format_version



## .allDocs()

### db.allDocs(options)

### Description
Does a GET request to "_all_docs" with the options as params.
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).

### Response
The total number of rows and an array of rows, each row containing one result of the query.



## .query()

### db.query(mapFun, reduceFun, language, options)

### Description
Applies the mandatory map function and the optional reduce function to the contents of database and returns the results. 
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).
The language of the query has to be specified when another language than the default JavaScript is used. [Erlang views have to be enabled](/http://wiki.apache.org/couchdb/EnableErlangViews) beforehand.

### Response
The total number of rows and an array of rows, each row containing one result of the query.

### Example
    db.query("function(doc) { emit(doc._id, null); }", null, "javascript", {})


## .view()

### db.view(viewname, options)

### Description
Applies the view to the contents of database and returns the results. When there are no keys given, it does a GET request to the view path with the options as params, or a POST request with the keys as body.
Options can include the [Querying Options of the HTTP view API](http://wiki.apache.org/couchdb/HTTP_view_API#Querying_Options).
The result can be specified more by querying only for single keys. Keys are part of the options hash.

### Response
The total number of rows and an array of rows, each row containing one result of the query, or null when the view doesn't exist.

### Example
    db.view('spec_db/viewname', {"include_docs":"true", "keys":["456"]})




## .getDbProperty()

### db.getDbProperty(propName, options, ajaxOptions)

### Description
Does a GET request to the db and the propName with the options as params.
  
### Response
The property value.

    

## .setDbProperty()

### db.setDbProperty(propName, propValue, options, ajaxOptions)

### Description
Does a PUT request to the db and the propName with the options as params and the propValue as body.
  
### Results
The db property is set to the specified value.

### Response
    {"ok" : true}

    