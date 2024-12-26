Here is a list of **important MongoDB CLI commands** that you can use to interact with the MongoDB shell, manage databases, collections, and documents, and perform administrative tasks.

### **1. General MongoDB Shell Commands**

- **Start the MongoDB Shell**:
  To start the MongoDB shell and connect to a running MongoDB instance, simply type:
  ```bash
  mongo
  ```

- **Show Available Databases**:
  To display a list of all databases on the MongoDB instance:
  ```javascript
  show databases;
  ```

- **Select a Database**:
  To switch to a specific database:
  ```javascript
  use <database_name>;
  ```

- **Show Collections in the Current Database**:
  To show all collections in the currently selected database:
  ```javascript
  show collections;
  ```

- **Exit the MongoDB Shell**:
  To exit the MongoDB shell:
  ```javascript
  exit;
  ```

---

### **2. Database Management**

- **Create a Database**:
  MongoDB does not require an explicit command to create a database. Simply switch to the database using `use <database_name>`, and MongoDB will create the database when you insert data into it.

- **Drop a Database**:
  To drop (delete) a database:
  ```javascript
  db.dropDatabase();
  ```

- **Get Database Statistics**:
  To get statistics about the current database:
  ```javascript
  db.stats();
  ```

---

### **3. Collection Management**

- **Create a Collection**:
  To create a collection explicitly:
  ```javascript
  db.createCollection("collection_name");
  ```

- **Show Collection Names**:
  To list all collections in the current database:
  ```javascript
  db.getCollectionNames();
  ```

- **Drop a Collection**:
  To drop (delete) a collection:
  ```javascript
  db.collection_name.drop();
  ```

- **Get Collection Statistics**:
  To get statistics about a specific collection:
  ```javascript
  db.collection_name.stats();
  ```

---

### **4. Document Operations**

- **Insert a Document into a Collection**:
  To insert a single document into a collection:
  ```javascript
  db.collection_name.insertOne({ key1: "value1", key2: "value2" });
  ```

  To insert multiple documents:
  ```javascript
  db.collection_name.insertMany([{ key1: "value1" }, { key2: "value2" }]);
  ```

- **Find Documents in a Collection**:
  To find all documents in a collection:
  ```javascript
  db.collection_name.find();
  ```

  To find documents with specific conditions:
  ```javascript
  db.collection_name.find({ key: "value" });
  ```

  To find one document:
  ```javascript
  db.collection_name.findOne({ key: "value" });
  ```

- **Update a Document**:
  To update a single document:
  ```javascript
  db.collection_name.updateOne({ key: "old_value" }, { $set: { key: "new_value" } });
  ```

  To update multiple documents:
  ```javascript
  db.collection_name.updateMany({ key: "old_value" }, { $set: { key: "new_value" } });
  ```

- **Replace a Document**:
  To replace a document entirely:
  ```javascript
  db.collection_name.replaceOne({ key: "value" }, { key: "new_value" });
  ```

- **Delete Documents**:
  To delete one document:
  ```javascript
  db.collection_name.deleteOne({ key: "value" });
  ```

  To delete multiple documents:
  ```javascript
  db.collection_name.deleteMany({ key: "value" });
  ```

- **Count Documents**:
  To count the number of documents in a collection or that match a specific condition:
  ```javascript
  db.collection_name.countDocuments();
  db.collection_name.countDocuments({ key: "value" });
  ```

---

### **5. Index Management**

- **Create an Index**:
  To create an index on a collection field:
  ```javascript
  db.collection_name.createIndex({ field_name: 1 });  // 1 for ascending, -1 for descending
  ```

  To create a compound index:
  ```javascript
  db.collection_name.createIndex({ field1: 1, field2: -1 });
  ```

- **Show Indexes**:
  To view all indexes on a collection:
  ```javascript
  db.collection_name.getIndexes();
  ```

- **Drop an Index**:
  To drop an index by its name:
  ```javascript
  db.collection_name.dropIndex("index_name");
  ```

---

### **6. Aggregation**

MongoDB’s aggregation framework allows you to perform complex data transformations and analysis.

- **Simple Aggregation (Group by Example)**:
  To count the number of documents grouped by a field:
  ```javascript
  db.collection_name.aggregate([
    { $group: { _id: "$field_name", count: { $sum: 1 } } }
  ]);
  ```

- **Match and Group Aggregation**:
  To filter and then group documents:
  ```javascript
  db.collection_name.aggregate([
    { $match: { status: "active" } },
    { $group: { _id: "$age", count: { $sum: 1 } } }
  ]);
  ```

- **Sort and Limit in Aggregation**:
  To sort the results and limit the number of documents:
  ```javascript
  db.collection_name.aggregate([
    { $sort: { age: 1 } },
    { $limit: 5 }
  ]);
  ```

---

### **7. Backup and Restore**

- **Backup (Mongodump)**:
  To create a backup of the MongoDB database, use the `mongodump` command from the shell (outside of MongoDB shell):
  ```bash
  mongodump --host <host> --port <port> --out <output_directory>
  ```

- **Restore (Mongorestore)**:
  To restore from a backup:
  ```bash
  mongorestore --host <host> --port <port> --dir <backup_directory>
  ```

---

### **8. Sharding Management Commands**

- **Enable Sharding for a Database**:
  To enable sharding for a specific database:
  ```javascript
  sh.enableSharding("myDatabase");
  ```

- **Shard a Collection**:
  To shard a collection based on a specific shard key:
  ```javascript
  sh.shardCollection("myDatabase.myCollection", { shardKeyField: 1 });
  ```

- **Add a Shard**:
  To add a shard to the cluster:
  ```javascript
  sh.addShard("hostname:port");
  ```

- **Move a Chunk to Another Shard**:
  To move a chunk from one shard to another:
  ```javascript
  sh.moveChunk("myDatabase.myCollection", { shardKeyField: value }, "targetShard");
  ```

---

### **9. User Management**

- **Create a User**:
  To create a new user in a database:
  ```javascript
  db.createUser({
    user: "username",
    pwd: "password",
    roles: [ { role: "readWrite", db: "myDatabase" } ]
  });
  ```

- **Show Users**:
  To list all users in the current database:
  ```javascript
  db.getUsers();
  ```

- **Drop a User**:
  To drop a specific user:
  ```javascript
  db.dropUser("username");
  ```

---

### **10. Replica Set Management (for Replication)**

- **Initiate a Replica Set**:
  To initiate a replica set:
  ```javascript
  rs.initiate();
  ```

- **Add a Member to Replica Set**:
  To add a new member to the replica set:
  ```javascript
  rs.add("hostname:port");
  ```

- **Check Replica Set Status**:
  To view the status of the replica set:
  ```javascript
  rs.status();
  ```

---

### **11. Server and Cluster Info**

- **Get Server Status**:
  To view the status of the MongoDB server:
  ```javascript
  db.serverStatus();
  ```

- **Get Server Build Info**:
  To view build information about the MongoDB server:
  ```javascript
  db.version();
  ```

---

### **12. Exit/Shutdown MongoDB Instance**

- **Exit the MongoDB Shell**:
  ```javascript
  exit;
  ```

- **Shutdown MongoDB Server** (admin user is required):
  ```javascript
  db.shutdownServer();
  ```

---

These commands provide a foundation for working with MongoDB through the MongoDB CLI. They cover basic operations like creating databases and collections, inserting and querying documents, as well as advanced operations like sharding and replica set management.