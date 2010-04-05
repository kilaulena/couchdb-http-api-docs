# Design Docs

## .allDesignDocs()

### CouchDB.allDesignDocs()

### Description
Goes through [all dbs](/allDbs) and returns all [design docs](/designDocs) for each db.

### Returns
An array with all dbs, for each db the id and revision of every design document.

### Example
When there is one database "test_db" and one design document "mydesign", the result is this:
    {"test_db": {"total_rows": 1, "offset": 0, "rows": [{"id": "_design/spec_db", "key": "_design/mydesign", "value": {"rev": "1-3885802b8f5804e8f03cda99df8e6cc7"}}]}}



## .designInfo()

### db.designInfo(docId)

### Description
Does a GET request to the db, the docId and "/_info". 

### Returns
The name of the design document and the view_index with the attributes: "signature", "language", "disk_size", "updater_running", "compact_running", "waiting_commit", "waiting_clients", "update_seq", "purge_seq"



## .designDocs()

### db.designDocs()

### Description
Does a GET request to "_all_docs" and filters out only the design documents.

### Returns
All design documents of a db.
