## Description
By default, TencentDB for MongoDB provides two user names "rwuser" and "mongouser" for the "MONGODB-CR" and "SCRAM-SHA-1" authentication methods respectively. The URI connection between these two authentication methods is different. For more information, see [Connection Example](https://intl.cloud.tencent.com/document/product/240/3563).

Node.js MongoDB Driver Documentation:
https://docs.mongodb.com/ecosystem/drivers/node/

## Quick Start
### Saample: Node.js native codes
Install driver package via Shell:
```
npm install mongodb --save
( In case of an unsuccessful installation, you can replace the source, npm config set registry http://registry.cnpmjs.org )
npm init
```
The application code:
```
'use strict';

var mongoClient = require('mongodb').MongoClient,
    assert = require('assert');

// Form the URI
var url = 'mongodb://mongouser:thepasswordA1@10.66.161.177:27017/admin';

mongoClient.connect(url, function(err, db) {
	assert.equal(null, err);
	var db = db.db('testdb'); // Select a "db"
	var col = db.collection('demoCol'); // Select a collection (table)
   // Insert data
    col.insertOne(
        {
            a: 1,
            something: "yy"
        },
        //Optional parameters
        //{
        //    w: 'majority' // Enable the "Majority" mode to ensure that data are written to the Secondary nodes
        //},
        function(err, r) {
            console.info("err:", err);
            assert.equal(null, err);
            // Assertion is written successfully
            assert.equal(1, r.insertedCount);
            // Query data
            col.find().toArray(function(err, docs) {
                assert.equal(null, err);
                console.info("docs:", docs);
                db.close();
            });
        }
    );
});
```

Output:

```
[root@VM_2_167_centos node]# node index.js
docs: [ { _id: 567a1bf26773935b3ff0b42a, a: 1, something: 'yy' } ]
```

## Sample codes of Connecting Node.js mongoose

```
var dbUri = "mongodb://" + user + ":" + password + "@" + host + ":" + port + "/" + dbName;
var opts = {
    auth: {
        authMechanism: 'MONGODB-CR', // This parameter is not required for SCRAM-SHA-1 authentication
        authSource: 'admin'
    }
};
var connection = mongoose.createConnection(dbUri, opts);
```

