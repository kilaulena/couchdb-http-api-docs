# Server

## .allDbs()

### CouchDB.allDbs()

### Description
Does a GET request to "_all_dbs". 

### Returns
An array with all the databases.


## .getVersion()

### CouchDB.getVersion()

### Description
Does a GET request to "/". 

### Returns
The version of the CouchDB installation.


## .replicate()

### CouchDB.replicate(source, target, replication_options)

### Description
Replicates the content of the source db to the target db. 
  
### Results
The target db contains all the documents from the source db.  

### Returns
    {"ok": true, "session_id": "a session id", "source_last_seq": 1, "history": [{"session_id": "a session id", "start_time": "start time", "end_time": "end time", "start_last_seq": 0, "end_last_seq": 1, "recorded_seq": 1, "missing_checked": 0, "missing_found": 1, "docs_read": 1, "docs_written": 1, "doc_write_failures": 0}]}
    
### Example
With the create_target option, the target db gets created if it doesn't already exist:
    CouchDB.replicate(http://localhost:5984/test_db, http://localhost:5984/test_db2, {"body" : {"create_target":true}})


## .newXhr()

### CouchDB.newXhr()

### Description
Returns an XMLHTTPRequest or an ActiveXObject, depending on the OS. If no XMLHTTPRequest support is detected, an error is thrown.

### Returns
A new XMLHTTPRequest or nothing.


## .request()

### CouchDB.request(method, uri, options)

### Description
Creates a [new XMLHTTPRequest](/newXhr). If the URI parameter doesn't start with "http://", the URI is prefixed with the CouchDB urlPrefix. If there are headers given in the options hash, they are set via setRequestHeader. The request is sent with the specified method. 

### Results
The XMLHTTPRequest has been sent with the given parameters.

### Returns
A new XMLHTTPRequest with readyState 4.

### Example
    CouchDB.request("GET", "/", {"headers": {"X-Couch-Full-Commit":"true"}});


## .requestStats()

### CouchDB.requestStats(module, key, test)

### Description
Does a GET request to "/_stats/module/key".

### Returns
Statistics about the specified module and key.

### Example
This returns the number of open databases:
    CouchDB.requestStats('couchdb', 'open_databases', test);
When the last argument is not null, "?flush=true" is appended to the request.


## .newUuids()

### CouchDB.newUuids(amount, buffer)

### Description
The CouchDB.uuids_cache is filled with as many UUIDs as specified in the buffer parameter, or with 100. The next time newUuids is called, they aren't requested from CouchDB, but taken directly from this cache, when the cache contains enough of them. 
  
### Returns
An array with the specified amount of UUIDs.

### Example
The first request gives you 10 UUIDs, the second 125. 
    CouchDB.newUuids(10);
    CouchDB.newUuids(125, 60);
The uuids_cache now contains 160 UUIDs.


## .maybeThrowError()

### CouchDB.maybeThrowError(request)

### Description
Throws an error when the given request has a status greater than 400. 

### Example
    var req = CouchDB.request("GET", "/nonexisting_db")
results in a 404 error, so 
    CouchDB.maybeThrowError(req)
returns
    {"error": "not_found", "reason": "no_db_file"}


## .params()

### CouchDB.params(options)

### Description
Turns a json object into a http params string.

### Returns
A string with the keys and values separated by "=" and "&" or an empty string when the options are empty.

### Example
    CouchDB.params({"key":"value", "key2":"value2"})
returns
    "key=value&key2=value2"

