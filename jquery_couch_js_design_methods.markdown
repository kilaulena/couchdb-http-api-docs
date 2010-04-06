# Design Docs

## .designDocs()

### db.designDocs(options)

### Description
Does a GET request to "_all_docs" and filters out only the design documents.

### Response
All design documents of a db.



## .allApps()

### db.allApps(options)

### Description
I goes through [every design document](/designDocs) in the db and looks if it  has an attachment with a member called "index.html" or a couchapp with a member called "index". If there is neither, it does nothing. If there is either, the "eachApp" method is called on each of those design documents.

The options hash has to contain an "eachApp" attribute that contains a custom function with this signature:
    eachApp: function(appName, appPath, ddoc)
The parameters being: 

* appName: the name of the design document
* appPath: the full path to the index member in the design document
* ddoc: the design document

### Results
The eachApp function is executed on every design document that has an "index" resp. "index.html" member.

### Example
    var designDoc = {"_id" : "_design/with_attachments"};
  
    designDoc._attachments = {
      "index.html" : {
        "content_type": "text\/html",
        // this is "<html><p>Hi, here is index!</p></html>", base64 encoded
        "data": "PGh0bWw+PHA+SGksIGhlcmUgaXMgaW5kZXghPC9wPjwvaHRtbD4="
      }
    };
    db.saveDoc(designDoc);
    
    db.allApps({
      eachApp: function(appName, appPath, ddoc) {
        // appName: "with_attachments"
        // appPath: "/spec_db/_design/with_attachments/index.html"
        // ddoc._id: "_design/with_attachments"
      }
    });