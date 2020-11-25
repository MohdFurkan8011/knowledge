# MongoDB

- [NoSQL Database](#nosql-databases)
- [MongoDB Introduction](#mongodb-introduction)
- [Features](#features-of-mongodb)
- [Data Types](#data-types)
- [Database Queries](#database-queries)
- [Collection](#Collection)
- [CRUD](#curd)
- [Interview QA](#interview-qa)



#### NoSQL Databases

We know that MongoDB is a NoSQL Database, so it is very necessary to know about NoSQL Database to understand MongoDB.

Databases can be divided in 3 types:

1. RDBMS (Relational Database Management System)
2. OLAP (Online Analytical Processing)
3. NoSQL (recently developed database)

##### Advantages of NoSQL

- It supports query language.
- It provides fast performance.
- It provides horizontal scalability.



#### MongoDB Introduction

**MongoDB** is a No SQL database. It is an open-source, cross-platform, document-oriented database written in C++.

**MongoDB** is an open-source document database that provides high performance, high availability, and automatic scaling.

In simple words, you can say that - Mongo DB is a document-oriented database. It is an open source product, developed and supported by a company named 10gen.

MongoDB is available under General Public license for free, and it is also available under Commercial license from the manufacturer.

**"MongoDB is a scalable, open source, high performance, document-oriented database." - 10gen**

##### Features of MongoDB

These are some important features of MongoDB:

1. Support - ad hoc queries In MongoDB, you can search by field, range query and it also supports regular expression searches.

2. Indexing - You can index any field in a document.

3. Replication - MongoDB supports Master Slave replication. A master can perform Reads and Writes and a Slave copies data from the master and can only be used for reads or back up (not writes)

4. Duplication of data - MongoDB can run over multiple servers. The data is duplicated to keep the system up and also keep its running condition in case of hardware failure.

5. Load balancing - It has an automatic load balancing configuration because of data placed in shards.

6. Supports map reduce and aggregation tools.

7. Uses JavaScript instead of Procedures.

8. It is a schema-less database written in C++.

9. Provides high performance.

10. Stores files of any size easily without complicating your stack.

11. Easy to administer in the case of failures.

12. It also supports:

    JSON data model with dynamic schemas

    Auto-sharding for horizontal scalability

    Built in replication for high availability

    

#### Data Types

| Data Types   | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| String       | String is the most commonly used datatype. It is used to store data. A string must be UTF 8 valid in mongodb. |
| Integer      | Integer is used to store the numeric value. It can be 32 bit or 64 bit depending on the server you are using. |
| Boolean      | This datatype is used to store boolean values. It just shows YES/NO values. |
| Double       | Double datatype stores floating point values.                |
| Min/Max Keys | This datatype compare a value against the lowest and highest bson elements. |
| Arrays       | This datatype is used to store a list or multiple values into a single key. |
| Object       | Object datatype is used for embedded documents.              |
| Null         | It is used to store null values.                             |
| Symbol       | It is generally used for languages that use a specific type. |
| Date         | This datatype stores the current date or time in unix time format. It makes you possible to specify your own date time by creating object of date and pass the value of date, month, year into it. |



##### Database Queries

- **Create** 

  There is no create database command in MongoDB. Actually, MongoDB do not provide any command to create database.

  It may be look like a weird concept, if you are from traditional SQL background where you need to create a database, table and insert values in the table manually.

  Here, in MongoDB you don't need to create a database manually because MongoDB will create it automatically when you save the value into the defined collection at first time.

  You also don't need to mention what you want to create, it will be automatically created at the time you save the value into the defined collection.

- **Use** 

  ```json
   >use database_name
  ```

- **Check current DB** 

  ```
  >db
  ```

- **Show database**

  ```
  >show dbs
  ```

- **Insert** 

  ```
  >db.collectionname.insert({"name": "Test"})
  ```

- **Drop database** 

  ```
  >db.dropDatabase();
  ```

  

#### Collection

In MongoDB, db.createCollection(name, options) is used to create collection. But usually you don? it need to create collection. MongoDB creates collection automatically when you insert some documents.

```
db.createCollection("collection_name", options)
```

Following is the list of options that can be used.

| Field       | Type    | Description                                                  |
| :---------- | :------ | :----------------------------------------------------------- |
| Capped      | Boolean | (Optional) If it is set to true, enables a capped collection. Capped collection is a fixed size collecction that automatically overwrites its oldest entries when it reaches its maximum size. If you specify true, you need to specify size parameter also. |
| AutoIndexID | Boolean | (Optional) If it is set to true, automatically create index on ID field. Its default value is false. |
| Size        | Number  | (Optional) It specifies a maximum size in bytes for a capped collection. Ifcapped is true, then you need to specify this field also. |
| Max         | Number  | (Optional) It specifies the maximum number of documents allowed in the capped collection. |

**Queries**

- To create collection

  ```
  >db.createCollection("SSSIT") 
  ```

- To check all collections

  ```
  >show collections
  ```

##### How does MongoDB create collection automatically

MongoDB creates collections automatically when you insert some documents.

```
>db.collection_name.insert({"name" : "seomount"})    
>show collections    
collection_name  
```



##### MongoDB Drop collection

In MongoDB, db.collection_name.drop() method is used to drop a collection from a database. It completely removes a collection from the database and does not leave any indexes associated with the dropped collections.

```
>db.collection_name.drop()
```



##### Curd

- **Insert**

  In MongoDB, the **db.collection.insert()** method is used to add or insert new documents into a collection in your database.

  ```
  > db.COLLECTION_NAME.insert({"name": "test"})
  
  > db.COLLECTION_NAME.insert([{"name": "test"}, {"name": "xyz"}])
  ```

  **Insert multiple documents with Bulk** 

  ```
  var bulk = db.collection_name.initializeUnorderedBulkOp();
  
  bulk.insert(  
     {  
       name: "abc"
     }
  );  
  
  bulk.execute();  
  ```

  

-  **Update**

  ```
  >db.COLLECTION_NAME.update(SELECTIOIN_CRITERIA, UPDATED_DATA)
  ```

  ```
  >db.collection_name.update({'name':'abc'},{$set:{'name':'xyz'}})
  ```

- **Delete**

  In MongoDB, the db.colloction.remove() method is used to delete documents from a collection. The remove() method works on two parameters.

  **1. Deletion criteria:** With the use of its syntax you can remove the documents from the collection.

  **2. JustOne:** It removes only one document when set to true or 1.

  **Remove all**

  ```
  > db.collection_name.remove({})  
  ```

  **Remove all documents that match a condition**

  ```
  > db.collection_name.remove( { type : "programming language" } )
  ```

  **Remove a single document that match a condition**

  ```
  > db.collection.remove( { type : "programming language" }, 1 )
  ```

  

- **Query**

  ```
  >db.collection.find()
  
  >db.collection.find({})
  ```



##### SQL and Mongo DB Select Command

| SQL SELECT Statement                                         | MongoDB find() Statement                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| SELECT * FROM table_name                                     | db.collection_name.find()                                    |
| SELECT id, user_id, status FROM table_name                   | db.collection_name.find( { }, { user_id: 1, status: 1 } )    |
| SELECT user_id, status FROM table_name                       | db.collection_name.find( { }, { user_id: 1, status: 1, _id: 0 } ) |
| SELECT * FROM table_name WHERE status = "A"                  | db.collection_name.find( { status: "A" } )                   |
| SELECT user_id, status FROM table_name WHERE status = "A"    | db.collection_name.find( { status: "A" }, { user_id: 1, status: 1, _id: 0 } ) |
| SELECT * FROM table_name WHERE status != "A"                 | db.collection_name.find( { status: { $ne: "A" } } )          |
| SELECT * FROM table_name WHERE status = "A" AND age = 50     | db.collection_name.find(    { status: "A",      age: 50 } )  |
| SELECT * FROM table_name WHERE status = "A" OR age = 50      | db.collection_name.find(    { $or: [ { status: "A" } , { age: 50 } ] } ) |
| SELECT * FROM table_name WHERE age > 25                      | db.collection_name.find(    { age: { $gt: 25 } } )           |
| SELECT * FROM table_name WHERE age < 25                      | Db.collection_name.find(   { age: { $lt: 25 } } )            |
| SELECT * FROM table_name WHERE age > 25 AND   age <= 50      | db.collection_name.find(   { age: { $gt: 25, $lte: 50 } } )  |
| SELECT * FROM table_name WHERE user_id like "%bc%"           | db.collection_name.find( { user_id: /bc/ } ) **or** db.collection_name.find( { user_id: { $regex: /bc/ } } ) |
| SELECT * FROM table_name WHERE user_id like "bc%"            | db.collection_name.find( { user_id: /^bc/ } ) **or** db.collection_name.find( { user_id: { $regex: /^bc/ } } ) |
| SELECT * FROM table_name WHERE status = "A" ORDER BY user_id DESC | db. collection_name. find( { status: "A" } ). sort( { user_id: -1 } ) |
| SELECT COUNT(*) FROM table_name                              | db. collection_name. count() **or** db. collection_name. find(). count() |
| SELECT COUNT(user_id) FROM table_name                        | db. collection_name.count( { user_id: { $exists: true } } ) **or** db. collection_name.find( { user_id: { $exists: true } } ).count() |
| SELECT COUNT(*) FROM table_name WHERE age > 30               | db. collection_name.count( { age: { $gt: 30 } } ) **or** db. collection_name.find( { age: { $gt: 30 } } ).count() |
| SELECT DISTINCT(status) FROM table_name                      | db. collection_name.aggregate( [ { $group : { _id : "$status" } } ] ) **or**, for distinct value sets that do not exceed the BSON size limit db. collection_name.distinct( "status" ) |
| SELECT * FROM table_name LIMIT 1                             | db. collection_name.findOne() **or** db. collection_name.find(). limit(1) |
| SELECT * FROM table_name LIMIT 5 SKIP 10                     | db. collection_name.find(). limit(5). skip(10)               |
| EXPLAIN SELECT * FROM table_name WHERE status = "A"          | db.collection_name.find( { status: "A" } ). explain()        |

##### SQL and MongoDB Update Statements

| SQL Update Statements                                  | MongoDB updateMany() Statements                              |
| :----------------------------------------------------- | :----------------------------------------------------------- |
| UPDATE table_name SET status = "C" WHERE age > 25      | db.collection_name.updateMany( { age: { $gt: 25 } }, { $set: { status: "C" } } ) |
| UPDATE table_name SET age = age + 3 WHERE status = "A" | db.collection_name.updateMany( { status: "A" } , { $inc: { age: 3 } } ) |



SQL and MongoDB Delete Statements

| SQL Delete Statements                     | MongoDB deleteMany() Statements                  |
| :---------------------------------------- | :----------------------------------------------- |
| DELETE FROM table_name WHERE status = "D" | db.collection_name.deleteMany( { status: "D" } ) |
| DELETE FROM table_name                    | db.collection_name.deleteMany( { } )             |





#### Interview QA