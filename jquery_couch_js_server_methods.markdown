# Intro
To get the results of all the methods, include these callbacks in the options hash, for example:
    $.couch.activeTasks({
      success: function(resp){ 
        console.log(resp); 
      },
      error: function(status, error, reason){
        console.log(status, error, reason);
      }
    });


# Server

## .activeTasks()

### $.couch.activeTasks(options)

### Description
Does a GET request to "_active_tasks". 

### Response
An array with all the active tasks, each entry containing type, PID, target and status of the task, or an empty array when there are no active tasks.


## .allDbs()

### $.couch.allDbs(options)

### Description
Does a GET request to "_all_dbs". 

### Response
An array with all the databases.



## .config()

### CouchDB.config(options, section, option, value)

### Description
Retreives or updates the server configuration.

### Results
When called with section, option and value, the option is updated to the value.
When called with section, option and null, the option is removed from the section.

### Response
* Without options: All the config settings
* With a section: The config section
* With a section, an option and a value: an empty string
* With a section, an option and null: the value the option had before

### Example
Gets all the config settings:
    $.couch.config();
Gets a specific config setting:
    $.couch.config({}, "couchdb");
Updates a config setting:
    $.couch.config({}, "couchdb", "max_dbs_open", "120");
Deletes a config setting:
    $.couch.config({}, "couchdb", "max_dbs_open", null);



## .info()

### CouchDB.info(options)

### Description
Does a GET request to "/". 

### Response
The version of the CouchDB installation.



## .replicate()

### CouchDB.replicate(source, target, ajaxOptions, replicationOptions)

### Description
Replicates the content of the source db to the target db. 
  
### Results
The target db contains all the documents from the source db.  

### Response
    {"ok": true, "session_id": "a session id", "source_last_seq": 1, "history": [{"session_id": "a session id", "start_time": "start time", "end_time": "end time", "start_last_seq": 0, "end_last_seq": 1, "recorded_seq": 1, "missing_checked": 0, "missing_found": 1, "docs_read": 1, "docs_written": 1, "doc_write_failures": 0}]}
    
### Example
With the create_target option, the target db gets created if it doesn't already exist:
    CouchDB.replicate(http://localhost:5984/test_db, http://localhost:5984/test_db2, {}, {"create_target":true})
    
    

## .newUUID()

### CouchDB.newUUID(cacheNum)

### Description
fill the uuidCache with the specified number minus 1
The CouchDB.uuidCache is filled with as many UUIDs as specified in the cacheNum parameter minus 1. The next time newUUID is called, the new UUID isn't requested from CouchDB, but taken directly from this cache if it's not empty.
  
### Response
A new UUID, either from the cache or from the server.



