# Documents

## .openDoc()

### db.open(docId, options, ajaxOptions)

### Description
Does a GET request to the db and the docId with the options as params.

### Response
The document. When the document doesn't exist, a 404 error is raised.


## .saveDoc()

### db.saveDoc(doc, options)

### Description
When the document doesn't contain an _id attribute it does a PUT request to the db and the docId with the options as params and the doc as body. 
When the document contains an _id attribute it does a POST request to the db with the options as params and the doc as body. 

### Results
A saved document with an ID. 

### Response
ID and revision of the saved document and
    {"ok" : true}



## .bulkSave()

### db.bulkSave(docs, options)

### Description
Does a POST request to the db and _bulk_docs with the options as params and the docs as body. 

### Results
All the documents are saved with an ID.

### Response
An array with an element for each document that contains ID and revision of the document.


     
## .removeDoc()

### db.removeDoc(doc)

### Description
Does a DELETE request to the db and the docId with the revision and the options as params. The current revision of the document has to be specified, otherwise the request results in a 409 error.

### Results
The document is deleted (that means the document has the "deleted":true attribute).

### Response
ID and revision of the deleted document and
    {"ok" : true}


    
## .bulkRemove()

### db.bulkRemove(docs, options)

### Description
Sets "_deleted" to true in each document. Then does a POST request to the db and _bulk_docs with the options as params and the docs as body. 

### Results
All the documents are deleted (that means the documents have the "deleted":true attribute).)

### Returns
An array with an element for each document that contains ID and revision of the deleted document.



## .copyDoc()

### db.copyDoc(docId, options, ajaxOptions)

### Description
Does a COPY request to the db and the docId.
The ajaxOptions hash has to contain a "headers" attribute, which has to contain a "Destination" attribute that specifies the ID that the new document should have.

### Results
Another document is saved that has the same data and the new ID.
When the new document already exists, its correct revision has to be provided in order to overwrite it. When there is no correct revision, an error is thrown.

### Response
The new document.
    
### Example
Copies a document with ID "123", the new document has ID "456":
    db.copyDoc("123", {}, {
      headers: {"Destination":"456"}
    });

When the new document already exists, its revision has to be part of the Destination:
    db.copyDoc("123", {}, {
      headers: {"Destination":"456?rev=" + revision_of_456}
    });
    
