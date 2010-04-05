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


