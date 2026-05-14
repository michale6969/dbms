# Assignment No. - 9

## Title

CRUD Operations using MongoDB.

## Problem Statement

Design and implement basic Create, Read, Update, and Delete (CRUD) operations using MongoDB. Use the save method and logical operators where necessary.

## Objective

- To learn concept of NOSQL.
- To implement CRUD operation in MOngoDB.

## Theory

- Difference between SQL and NOSQL

### NOSQL

A NoSQL (originally referring to "non SQL" or "non relational") database provides a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases. Such databases have existed since the late 1960s, but did not obtain the "NoSQL" moniker until a surge of popularity in the early twenty-first century, triggered by the needs of Web 2.0 companies such as Facebook, Google, and Amazon.com. NoSQL databases are increasingly used in bigdata and real-time web applications. [6] NoSQL systems are also sometimes called "Not only SQL" to emphasize that they may support SQL-like query languages. Motivations for this approach include: simplicity of design, simpler "horizontal" scaling to clusters of machines (which is a problem for relational databases), [2] and finer control over availability. The datastructures used by NoSQL databases (e.g. key-value, wide column, graph, or document) are different from those used by default in relational databases, making some operations faster in NoSQL. The particular suitability of a given NoSQL database depends on the problem it must solve. Sometimes the data structures used by NoSQL databases are also viewed as "more flexible" than relational database tables. Many NoSQL stores compromise consistency (in the sense of the CAP theorem) in favor of availability,partition tolerance, and speed. Barriers to the greater adoption of NoSQL stores include the use of low- level query languages (instead of SQL, for instance the lack of ability to perform ad-hoc joins across tables), lack of standardized interfaces, and huge previous investments in existing relational databases. Most NoSQL stores lack true ACID transactions, although a few databases, such as MarkLogic, Aerospike, FairCom c-treeACE, Google Spanner (though technically a NewSQL database), Symas LMDB, and OrientDB have made them central to their designs. (See ACID and join support.)

### MongoDB

MongoDB is a cross-platform, document oriented database that provides, high performance, high availability, and easy scalability. MongoDB works on concept of collection and document. Database Database is a physical container for collections. Each database gets its own set of files on the filesystem. A single MongoDB server typically has multiple databases.

### Collection

Collection is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database. Collections do not enforce a schema. Documents within a collection canhave different fields. Typically, all documents in a collection are of similar or related purpose.

### Document

A document is a set of key-value pairs. Documents have dynamic schema. Dynamic schema means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.

### Sample Document

Following example shows the document structure of a VisionX session, which is simply a comma separated key value pair.

```javascript
{
  _id: ObjectId("7df78ad8902c"),
  session_id: 501,
  device_code: 'VX-ESP-01',
  session_state: 'COMPLETE',
  frame_count: 3840,
  recording: { snapshot_path: 'runtime_data/artifacts/session-0501/snapshot.jpg' },
  analysis_results: [{ kind: 'face', status: 'completed' }, { kind: 'general', status: 'completed' }],
  session_events: [{ event_type: 'session.streaming', message: 'Streaming started' }]
}
```

_id is a 12 bytes hexadecimal number which assures the uniqueness of every document. You can provide _id while inserting the document. If you don‟t provide then MongoDB provides a unique id for every document. These 12 bytes first 4 bytes for the current timestamp, next 3 bytes for machine id,next 2 bytes for process id of MongoDB server and remaining 3 bytes are simple incremental VALUE.

### MongoDB ─ Advantages

Any relational database has a typical schema design that shows number of tables and the relationshipbetween these tables. While in MongoDB, there is no concept of relationship. Advantages of MongoDB over RDBMS Schema less: MongoDB is a document database in which one collection holds different documents. Number of fields, content and size of the document can differ from one document to another. Structure of a single object is clear..0 No complex joins. Deep query -ability. MongoDB supports dynamic queries on documents using a document-based query language that's nearly as powerful as SQL. Tuning. Ease of scale -out: MongoDB is easy to scale. Conversion/mapping of application objects to database objects not needed. Uses internal memory for storing the (windowed) working set, enabling faster access of data. Why Use MongoDB-> Document Oriented Storage: Data is stored in the form of JSON style documents. Index on any attribute Replication and high availability Auto-sharding Rich queries Fast in-place updates Professional support by MongoDB Where to Use MongoDB-> Big Data Content Management and Delivery Mobile and Social Infrastructure User Data Management Data Hub MongoDB Help To get a list of commands, type db.help() in MongoDB client. This will give you a list of commands as shown in the following screenshot.

### The use Command

MongoDB use DATABASE_NAME is used to create database. The command will create a new database if it doesn't exist, otherwise it will return the existing database.

#### Syntax

```js
use DATABASE_NAME
```

If you want to create a database with name `<visionx_db>`, then use DATABASE statement would be as follows.

#### Example

```js
> use visionx_db
switched to db visionx_db
> db
> show dbs
local 0.78125 GB
test 0.23012 GB
Your created database (mydb) is not present in list. To display database, you need to insert at least one document into it.
> db.visionx_devices.insert({"device_code":"VX-ESP-01"})
```

In MongoDB default database is test. If you didn't create any database, then collections will be stored in test database.

### The dropDatabase() Method

MongoDB db.dropDatabase() command is used to drop a existing database.

#### Syntax

```js
db.dropDatabase()
```

### The createCollection() Method

MongoDB db.createCollection(name, options) is used to create collection.

#### Syntax

```js
db.createCollection(name, options)
```

In the command, name is name of collection to be created. Options is a document and is used to specify configuration of collection.

Parameter Type Description Name String Name of the collection to be created Options Document (Optional) Specify options about memorySize and indexing.

### The drop() Method

MongoDB's db.collection.drop() is used to drop a collection from the database.

#### Syntax

```js
db.COLLECTION_NAME.drop()
```

### MongoDB Datatypes

String: This is the most commonly used datatype to store the data. String in MongoDB must be UTF-8 valid. Integer: This type is used to store a numerical value. Integer can be 32 bit or 64 bit depending upon your server. Boolean: This type is used to store a boolean (true/ false) value. Double: This type is used to store floating point values. Min/Max Keys: This type is used to compare a value against the lowest and highest BSONelements. Arrays: This type is used to store arrays or list or multiple values into one key. Timestamp: ctimestamp. This can be handy for recording when a document has been modified or added. Object: This datatype is used for embedded documents. Null: This type is used to store a Null value. Symbol: This datatype is used identically to a string; however, it's generally reserved for languages that use a specific symbol type. Date: This datatype is used to store the current date or time in UNIX time format. You can specify your own date time by creating object of Date and passing day, month, year into it. Object ID: This datatype is used to store the document‟s ID. Binary data: This datatype is used to store binary data. Code: This datatype is used to store JavaScript code into the document. Regular expression: This datatype is used to store regular expression.

### MongoDB ─ Insert Document

The insert() Method To insert data into MongoDB collection, you need to use MongoDB's insert() or save() method.

#### Syntax

```js
>db.COLLECTION_NAME.insert(document)
```

#### Example

```javascript
db.visionx_devices.insert({
  device_code: "VX-ESP-01",
  device_name: "VisionX Lab Glasses",
  current_status: "IDLE"
})
```

### MongoDB ─ Query Document

The find() Method To query data from MongoDB collection, you need to use MongoDB's find() method.

#### Syntax

```js
>db.COLLECTION_NAME.find()
```

find() method will display all the documents in a non-structured way. The pretty() Method To display the results in a formatted way, you can use pretty() method.

#### Syntax

```js
>db.mycol.find().pretty()
```

Apart from find() method, there is findOne() method, that returns only one document.

#### Example

```javascript
db.visionx_sessions.find().pretty()
db.visionx_sessions.findOne({session_id: 501})
```

### RDBMS Where Clause Equivalents in MongoDB

To query the document on the basis of some condition, you can use following operation.

#### AND in MongoDB

In the find() method, if you pass multiple keys by separating them by ',' then MongoDB treats it as AND condition. Following is the basic syntax of AND −

```js
>db.mycol.find({key1:value1, key2:value2}).pretty()
```

#### OR in MongoDB

To query documents based on the OR condition, you need to use $or keyword. Following is the basic syntax of OR −

```js
>db.mycol.find({ $or: [ {key1: value1}, {key2:value2} ] }).pretty()
```

#### Using AND and OR Together

The following example will show the documents that have frame_count greater than 1000 and whose session_state is either 'ERROR' or device_code is 'VX-ESP-01'. Equivalent SQL where clause is `where frame_count>1000 AND (device_code = 'VX-ESP-01' OR session_state = 'ERROR')`.

```javascript
db.visionx_sessions.find({
  "frame_count": {$gt:1000},
  $or: [{"device_code": "VX-ESP-01"}, {"session_state": "ERROR"}]
}).pretty()
```

```json
{ "session_id": 501,
  "device_code": "VX-ESP-01",
  "session_state": "COMPLETE",
  "frame_count": 3840,
  "analysis_results": [{ "kind": "face", "status": "completed" }] }
```

### MongoDB Update() Method

MongoDB's update() and save() methods are used to update document into a collection. The update() method updates the values in the existing document while the save() method replaces the existing document with the document passed in save() method.

#### Syntax

```js
>db.COLLECTION_NAME.update(SELECTIOIN_CRITERIA, UPDATED_DATA)
```

### MongoDB Save() Method

The save() method replaces the existing document with the new document passed in the save() method.

#### Syntax

```js
>db.COLLECTION_NAME.save({_id:ObjectId(),NEW_DATA})
```

#### Example

```javascript
db.visionx_sessions.update(
  {session_id: 502},
  {$set: {session_state: 'PROCESSING'}}
)
db.visionx_sessions.save({
  session_id: 502,
  device_code: 'VX-ESP-01',
  session_state: 'PROCESSING',
  frame_count: 920
})
```

### The remove() Method

MongoDB's remove() method is used to remove a document from the collection. remove() method accepts two parameters. One is deletion criteria and second is justOne flag. deletion criteria: (Optional) deletion criteria according to documents will be removed. justOne: (Optional) if set to true or 1, then remove only one document.

#### Syntax

```js
>db.COLLECTION_NAME.remove(DELETION_CRITERIA)
```

### Remove Only One

If there are multiple records and you want to delete only the first record, then set justOne parameter in remove() method.

```javascript
db.visionx_sessions.remove({session_id:502},1)
```

### Remove All Documents

If you don't specify deletion criteria, then MongoDB will delete whole documents from the collection. This is equivalent of SQL's truncate command.

```javascript
db.visionx_temp_events.remove()
db.visionx_temp_events.find()
```

```js
>db.mycol.find()
```

### The Limit() Method

To limit the records in MongoDB, you need to use limit() method. The method accepts one number type argument, which is the number of documents that you want to be displayed.

#### Syntax

```js
>db.COLLECTION_NAME.find().limit(NUMBER)
```

### MongoDB Skip() Method

Apart from limit() method, there is one more method skip() which also accepts number type argument and is used to skip the number of documents.

#### Syntax

```js
db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
```

### The sort() Method

To sort documents in MongoDB, you need to use sort() method. The method accepts a document containing a list of fields along with their sorting order. To specify sorting order 1 and -1 are used. 1 is used for ascending order while -1 is used for descending order.

#### Syntax

```js
>db.COLLECTION_NAME.find().sort({KEY:1})
```

#### Example

```javascript
db.visionx_sessions.find().limit(5).skip(1)
db.visionx_sessions.find().sort({started_at:-1})
```

### Installation steps

```python
download the software “mongodb-linux-x86_64-3.4.9.tgz”
Copy to Download
[root@localhost Downloads]# tar -xvzf mongodb-linux-x86_64-3.4.9.tgz
[root@localhost Downloads]# cd mongodb-linux-x86_64-3.4.9/
[root@localhost mongodb-linux-x86_64-3.4.9]# cd bin
[root@localhost bin]# ./mongod -dbpath /home/admin/
[root@localhost bin]# ./mongo
```

### Installation steps in Windows

```python
Install MongoDB setup
Open "C:\Program Files (x86)\MongoDB\Server\3.0\bin"

mongod.exe ==> Server file || mongo.exe ==> Client file

Create Folder like "D:\TE\data\db"
Run MongoDB Server -> Open Command prompt as Administrator
> cd C:\Program Files (x86)\MongoDB\Server\3.0\bin
> mongod.exe --dbpath "D:\TEB\data\db"

Run MongoDB Client -> Open Second Command prompt
> cd C:\Program Files (x86)\MongoDB\Server\3.0\bin
> mongo.exe
```

## Conclusion

Thus we have studied the concept NOSQL-MongoDB and implemented.

## FAQ

1. What makes MongoDB the best?
2. If you remove an object attribute, is it deleted from the database? Explain with example.
3. How does MongoDB provide consistency?
4. Define MongoDB.
5. What are the key features of MongoDB?
6. Which command is use to create database? Explain with example.
7. Which command is use to drop database? Explain with example.
8. What is the use of pretty() method? Explain with example.
9. Which method is used to remove the document form the collection? Explain with example.
