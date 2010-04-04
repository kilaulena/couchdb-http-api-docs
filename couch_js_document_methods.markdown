# Documents

## .save()

### db.save(doc, options)

### Description
Sets a docId when the document doesn't contain an _id attribute. Then does a PUT request to the docId with the options as params and the doc as body. 

### Results
A saved document with an ID. 

### Returns
ID and revision of the saved document.

### Example
    db.save(doc, {"batch" : "ok"})
    

## .open()

### db.open(docId, options)

### Description
Does a GET request to the docId with the options as params.

### Returns
The document, or null when the document doesn't exist.

### Example
    db.open("123", {"revs" : "true"})
     
     
## .deleteDoc()

### db.deleteDoc(doc)

### Description
Does a DELETE request to the docId with the revision as param. The current revision of the document has to be specified, otherwise the request results in a 409 error.

### Results
The document is deleted (that means the document has the "deleted":true attribute).

### Returns
ID and revision of the deleted document.

### Example
    db.deleteDoc({_id : "123", _rev : "1-04d86233b3254bb5a53dcf7103f97fc2"})
     
     
     
## .deleteDocAttachment()

### db.deleteDocAttachment(doc, attachment_name)

### Description
Does a DELETE request to the docId and the attachment_name with the revision as param. The current revision of the document has to be specified, otherwise the request results in a 409 error.

### Results
The attachment is deleted, the document stays intact otherwise.

### Returns
ID and revision of the document whose attachment has been deleted.

### Example
    db.deleteDocAttachment({_id : "123", _rev : "1-04d86233b3254bb5a53dcf7103f97fc2"}, "attachment.txt")
     

     
## .bulkSave()

### db.bulkSave(docs, options)

### Description
Sets a docId in each document when it doesn't contain an _id attribute. Then does a POST request to the _bulk_docs with the docs and the options as body. 

### Results
All the documents are saved with an ID.

### Returns
An array with an element for each document that contains ID and revision of the document.

### Example
    doc1 = {"foo":"bar"}
    doc2 = {"foo":"baz"}
    db.bulkSave([doc1, doc2])
    
