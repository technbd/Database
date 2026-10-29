## MongoDB Interview Questions:

MongoDB is a NoSQL, document-oriented database that stores data in BSON (Binary JSON) format. It is designed for flexible data modeling, high availability, horizontal scalability, and efficient data processing.

_Main Features of MongoDB:_
- Document-Oriented :	Stores data as BSON documents instead of relational rows.
- Flexible Schema :	Documents in the same collection can have different fields and structures.
-	High Availability :	Replica sets provide redundancy and automatic failover.
-	Horizontal Scalability :	Sharding distributes data across multiple servers.
-	Indexing :	Supports single-field, compound, multikey, text, geospatial, TTL, and other indexes.
-	Aggregation : Pipeline	Supports filtering, grouping, sorting, joining, and transforming data.
-	Replication	: Copies data between replica-set members using the oplog.
-	Sharding :	Distributes large datasets and workloads across shards.
-	Transactions :	Supports atomic single-document operations and multi-document transactions.
-	High Performance :	Indexes and suitable data models can improve read and write performance.
-	Flexible Queries :	Supports filtering, projections, sorting, and complex query operators.
-	Security :	Supports authentication, role-based access control, TLS, and auditing features where configured and supported.
-	Backup and Recovery :	Supports logical backups with mongodump and restores with mongorestore; other backup methods are available.
-	Change Streams	Allows applications to subscribe to database changes.
-	Cross-Platform Support :	Runs on supported Linux, Windows, and macOS environments.
-	Cloud Support :	MongoDB Atlas provides a managed cloud database service.


### What is MongoDB?

MongoDB is an open-source, document-oriented NoSQL database that stores data in flexible, JSON-like (BSON) format instead of traditional rows and tables. It supports flexible schemas, indexing, replication, sharding, and aggregation.

_How does MongoDB differ from relational databases (RDBMS)?_
- **Schema**: RDBMS uses a rigid, predefined schema; MongoDB uses a dynamic, flexible schema.
- **Structure**: RDBMS stores data in tables of rows and columns; MongoDB stores data as documents in collections.
- **Scaling**: RDBMS scales vertically (bigger servers); MongoDB scales horizontally via sharding.
- **Relationships**: RDBMS uses foreign keys and joins; MongoDB typically uses **embedding** or **referencing**.



### What is MongoDB Atlas?

MongoDB Atlas is MongoDB's managed cloud database service. It provides database deployment, monitoring, backups, scaling, and security features.

MongoDB Atlas is a fully managed cloud database service provided by MongoDB. It offers automated deployment, scaling, and management of MongoDB clusters across various cloud providers (AWS, Azure, Google Cloud).



### What is MongoDB Compass?

MongoDB Compass is the official graphical user interface (GUI) for MongoDB. It allows database administrators and developers to connect to MongoDB servers, browse documents, execute queries, manage indexes, build aggregation pipelines, and analyze query performance without relying entirely on the command line.


### What are the advantage of MongoDB over relational databases?
Advantages include scalability, flexibility, ease of development, high performance for certain workloads.



### What is the difference between SQL and MongoDB?

| SQL Database |	MongoDB |
| ------------ |	------- |
| Relational database |	Document-oriented database |
| Table       |	Collection |
| Row         |	Document  | 
| Column      |	Field     | 
| Primary key |	`_id` field | 
| JOIN	      | `$lookup` or application-side joins | 
| Fixed or predefined schema |	Flexible schema | 
| SQL queries |	MongoDB Query Language (MQL) | 




### What data types are supported in MongoDB documents?
MongoDB supports a variety of BSON data types, which extend standard JSON types:

- **String** – Text data like `name: "Rahim"`.
- **Number** – Integer (int), Long (long), Double (double), Decimal (Decimal128) like 
    - `age: NumberInt(30)` // 32-bit Integer
    - `rating: 4.5` // Double
    - `salary: NumberDecimal("50000.75")`  // Decimal128
- **Boolean** – true or false like `active: true`.
- **Null** – Represents a null value like `middleName: null`.
- **Array** – List of values (can store mixed types) like `skills: ["Linux", "MongoDB"]`.
- **Date** – Stores date and time in UTC format like `createdAt: ISODate("2026-10-29T00:00:00Z")`.
- **Timestamp** – Special internal type used for replication and sharding.
- **Binary Data** – Stores binary data like images or files.
- **Object / Embedded Document** – Nested documents within a document.
- **ObjectId** – Unique identifier automatically generated for _id field.
- **Regular Expression** – For pattern matching.
- **Code / JavaScript** – Stores JavaScript code.


### What is BSON?
BSON stands for Binary JSON. MongoDB uses it internally to store documents. It supports additional types such as `ObjectId`, `Date`, `Decimal128`, and binary data.

BSON (Binary JSON) is the binary-encoded serialization of JSON-like documents that MongoDB uses for internal storage and data transfer. It supports extra data types like Date and BinData that standard JSON lacks, and allows fast traversal.


### What is the maximum BSON document size?

The maximum BSON document size is **16 MiB**. Large files can be stored using GridFS or an external object-storage system.

### How does MongoDB store data internally?
MongoDB stores data in BSON (Binary JSON) format, which is optimized for speed and traversing. Collections are stored in databases as files on disk using the WiredTiger storage engine.



### Explain the concept of a collection and a document in MongoDB.

#### Collection:
A collection is a group of MongoDB documents, similar to a table in a relational database.
- A collection is a group of documents in MongoDB.
- It is similar to a table in relational databases, but schema-less.
- All documents in a collection are stored together and can be queried collectively.
- Example: A users collection may contain multiple documents like the one above.


_Create new or switch to a database:_
```JavaScript
db.hello()
show dbs

use db1
db
db.stats()
db.currentOp()
```


_Create a collection:_
```JavaScript
db.createCollection("myCollection")
db.createCollection("employees")

show collections
```



#### Document:
A document is a set of key-value pairs stored in BSON format (like JSON).
- A document is the basic unit of data in MongoDB.
- It is a JSON-like object (stored as BSON internally) containing key-value pairs.
- Each document can have different fields and nested structures.



_Insert a document:_
```JavaScript
db.myCollection.insertOne({ name: "Alice", age: 25, city: "New York" })

//Insert multiple documents:
db.myCollection.insertMany([
  { name: "Bob", age: 30, city: "Los Angeles" },
  { name: "Charlie", age: 35, city: "Chicago" }
])
```



_Update a document:_
```JavaScript
db.myCollection.updateOne(
  { name: "Alice" },
  { $set: { age: 31 } }
)
```




_Retrieve documents:_
```JavaScript
// All documents
db.myCollection.find()

// Specific condition
db.myCollection.find({ age: 31 })
```



```JavaScript
  {
    _id: ObjectId('6ae2e1a68b17df29002f90db'),
    name: 'Alice',
    age: 31,
    city: 'New York'
  }
```




### How do you count documents?

```JavaScript
db.myCollection.count();

//or,

db.myCollection.countDocuments();

db.myCollection.countDocuments({ name: "Alice" })
```



### What is a Capped Collection in MongoDB?

A capped collection is a fixed-size collection in MongoDB that maintains documents in insertion order. When the collection reaches its configured size limit, MongoDB automatically overwrites the oldest documents as new documents are inserted.

Capped collections are useful for logs, event tracking, and recent activity data where only a limited amount of historical information needs to be retained.

> Individual document deletion with `deleteOne()` or `deleteMany()` is not supported for capped collections.





### What is the role of the `_id` field?

`_id` uniquely identifies each document within a collection. It acts as the default primary key and helps in indexing and quick retrieval.

The `_id` field acts as the **primary key** for every document in a MongoDB collection. If you do not provide one during an insert, MongoDB **automatically generates a unique 12-byte** `ObjectId`.

- Every standard MongoDB document has a unique _id field.
- MongoDB automatically generates an ObjectId if you omit it during insertion.
- The _id field has a unique index by default.
- You cannot change _id after inserting a document.




### What is a schema in MongoDB?

An index is a data structure that helps MongoDB find documents without scanning the entire collection. Indexes improve query performance but consume disk space and increase write overhead.

A schema defines the structure and validation rules for documents. MongoDB allows flexible schemas, but schema validation can enforce field types and required fields.



### What is an Index and why do you use it?
An index is a data structure that stores a small portion of the collection's data in an easy-to-traverse form. Without indexes, MongoDB must perform a **collection scan** (inspecting every single document) to fulfill a query.

An index in MongoDB is a data structure that improves the speed of data retrieval operations on a collection. 


### What types of indexes does MongoDB support?

| Index type	| Purpose |
| ----------	| ------- |
| **Single-field** |	Index one field |
| **Compound** |	Index multiple fields | 
| **Multikey** |	Index array values | 
| **Text** |	Text search |
| **Geospatial** |	Location-based queries |
| **Hashed** |	Hash-based indexing, often used in sharding | 
| TTL |	Automatically expire eligible documents |
| Unique |	Enforce uniqueness | 



### How do you create an index?

```JavaScript
// Single-field index
db.myCollection.createIndex({ name: 1 })

//List indexes
db.myCollection.getIndexes()
```




### What is the difference between COLLSCAN and IXSCAN?

| COLLSCAN | IXSCAN |
| -------- | ------ |
| Scans collection documents |	Scans index entries |
| May be expensive on large collections |	Often faster for selective queries |
| Can be appropriate for small collections or queries matching most documents | Depends on index suitability and query selectivity |



### What is Journaling in MongoDB?
Journaling in MongoDB is a mechanism that records changes to the database in a journal file before those changes are permanently written to the data files. It helps MongoDB recover data after an unexpected shutdown, system crash, or power failure.

_How MongoDB Journaling Works:_
```
              1. Write Operation
An application inserts, updates, or deletes a document.


              2. Write to Journal
MongoDB records the changes in the journal on disk.


              3. Acknowledge the Write
Depending on the write concern and journaling settings, MongoDB can acknowledge the operation once the required durability conditions are met.


              4. Write to Data Files
Changes are eventually written to the main database data files.
```


_How to Check Journaling in MongoDB:_
```
db.serverStatus().storageEngine


{
  name: 'wiredTiger',
  supportsCommittedReads: true,
  oldestRequiredTimestampForCrashRecovery: Timestamp({ t: 0, i: 0 }),
  supportsPendingDrops: true,
  dropPendingIdents: Long('0'),
  supportsSnapshotReadConcern: true,
  readOnly: false,
  persistent: true,
  backupCursorOpen: false
}
```



### Types of MongoDB Storage Engines:

1. **WiredTiger (Default)**:
    - Default and recommended storage engine since MongoDB 3.2.
    - Document-level locking (optimistic concurrency control), allowing multiple clients to modify different documents in the same collection simultaneously.
    - Supports document-level concurrency, compression, checkpoints, and journaling.
2. **In-Memory Storage Engine**:
    - Stores data in memory for low-latency access; availability depends on MongoDB edition and version.
    - Document-level locking, similar to WiredTiger.
    - Ideal for real-time analytics, high-frequency trading, caching layers, or scenarios where predictable ultra-low latency matters more than on-disk persistence.
3. **MMAPv1 (Legacy / Deprecated)**: 
    - Older storage engine that used memory-mapped files.
    - MongoDB's original storage engine; deprecated and removed in versions after MongoDB 3.2/3.4.
    - Collection-level locking (improved from earlier global locks, allowing multiple readers or a single writer per collection).



### What is the Role of Journaling in MongoDB, and How Does It Impact Performance?

Journaling in MongoDB ensures data durability and crash recovery by writing changes to a journal file before updating the actual database files. In case of a crash, MongoDB replays the journal to restore data consistency. While it improves data safety, it may slightly affect performance due to extra disk I/O operations.


### MongoDB provides several mechanisms to ensure data consistency:

MongoDB maintains data consistency through **replica-set replication**, **write concern**, **read concern**, **read preference**, **atomic operations**, and **transactions**.

- **Journaling**: MongoDB uses write-ahead logging to maintain data integrity.
- **Write Concerns**: Define how many nodes must acknowledge a write (e.g., primary only or primary + secondaries).
- **Replica Sets**: Replicate data across nodes to ensure availability and consistency, with read concerns controlling read consistency.


#### Replica-set replication:
MongoDB replicates changes from the primary to secondary members using the **oplog (operations log)**.
- The primary accepts writes under normal operation.
- Secondary members replicate and apply those operations.
- Replication is asynchronous by default.
- A secondary may return older data if it has not yet applied recent writes.



#### Write concern:
Write concern determines how much acknowledgment MongoDB requires before considering a write successful.

Write Concern in MongoDB defines how many nodes must acknowledge a write before it is considered successful, with levels like acknowledged (default), unacknowledged, journaled, and replica-acknowledged.

_Importance of Write Concern:_
- Balances data durability and performance.
- Higher write concern ensures data is safely written and replicated.
- Lower write concern improves performance with less acknowledgment.
- Helps control latency based on application reliability needs.




#### Read concern:
Read concern determines the consistency guarantees for data returned by a read.
- `local`	: Returns the node's locally available data; it may include data not yet majority committed
- `majority` :	Returns data acknowledged as majority committed
- `linearizable` :	For supported primary reads, provides real-time ordering guarantees for majority-committed writes
- `available` :	Returns locally available data, with different guarantees from majority reads
- `snapshot` :	Provides a consistent snapshot, particularly useful in transactions




#### Read preference:
Read preference determines which replica-set member handles a read.
- `primary` :	Reads from the primary
- `primaryPreferred` :	Prefers the primary
- `secondary` :	Reads from secondary members
- `secondaryPreferred` :	Prefers secondaries
- `nearest` :	Selects a suitably eligible member with low network latency



#### Atomic operations:
MongoDB guarantees atomicity at the single-document level, including updates to multiple fields within the same document.


#### Transactions:
Multi-document transactions allow a group of operations to commit or abort together.





### What is the difference between mongosh, mongodump, and mongorestore?

| Tool	| Purpose |
| ---	| ------- |
| `mongo` (deprecated) |	The old MongoDB shell (used before MongoDB 5.0). | 
| `mongosh` (new shell) |	Interactive MongoDB shell | 
| `mongodump` |	Creates logical backups |
| `mongorestore` |	Restores logical backups |




### How Does MongoDB Ensure High Availability and Scalability?
- MongoDB ensures high availability and scalability through its features like **replica sets** and **sharding**.
- **Replica sets** provide redundancy and failover capabilities by ensuring that data is always available.
- **Sharding** distributes data across multiple servers, enabling horizontal scalability to handle large volumes of data and high traffic loads.



### What is a Replica Set?

A replica set is a group of `mongod` instances that maintain the **same dataset** through replication. It includes a **primary node** (handles writes) and multiple **secondary nodes** (replicate data).

- A replica set in MongoDB is a group of mongod instances that maintain the same data set.
- A replica set consists of a primary node and multiple secondary nodes.
- The primary node receives all write operations while secondary nodes replicate the primary's data and can serve read operations.
- If the primary node fails, an automatic election process selects a new primary to maintain high availability.



```yaml
# mongod.conf

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# Where and how to store data.
storage:
  dbPath: /var/lib/mongo
  journal:
    enabled: true
#  engine:
#  wiredTiger:

# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

# network interfaces
net:
  port: 27017
  bindIp: 0.0.0.0

replication:
  replSetName: rs0
```


### What is the difference between primary and secondary nodes?
- **Primary**: receives writes under normal replica-set operation.
- **Secondary**: replicates the primary's operations through the oplog.
- **Arbiter**: participates in elections but does not store the dataset.


### What is the oplog?

The oplog (operations log) is a capped collection named `local.oplog.rs` on replica-set members. It records operations used to replicate changes to secondary members.

_Check oplog information:_
```
rs.printReplicationInfo()
```


### What is a MongoDB election?

An election determines which eligible replica-set member becomes primary. Elections can occur after failures, network partitions, or certain configuration changes. Elections may cause a short write interruption.



### What happens if the primary node fails?

The remaining eligible voting members hold an election. If a majority of voting members is available, an eligible secondary can become primary.

Applications using a replica-set-aware connection string can discover the new primary and reconnect, subject to driver configuration and retry behavior.




### What is Sharding?
Sharding is MongoDB’s method for horizontal scaling. It partitions large datasets across multiple physical servers or clusters (shards) using a chosen shard key.

Sharding distributes a collection's documents across multiple shards. MongoDB uses a shard key to determine how data is distributed.

A typical sharded cluster includes:
- Shards, commonly replica sets.
- Config servers, deployed as a config-server replica set.
- `mongos` query routers.



### What is the difference between replication and sharding?

| Replication |	Sharding |
| ----------- |	-------- |
| Maintains copies of data |	Distributes data across shards |
| Provides redundancy and high availability |	Provides horizontal scaling and data distribution |
| Each data-bearing member has the replica-set dataset |	Each shard holds a portion of the overall dataset |
| Does not by itself increase write capacity by splitting data |	Can distribute write and storage load |




### What are the advantages and disadvantages of sharding?

Advantages include scalability and improved performance. Disadvantages include increased complexity and potential overhead for managing shards.



### How to Implement Access Control and User Authentication in MongoDB?

Access control and user authentication in MongoDB are implemented through a role-based access control (RBAC) system. You create users and assign roles that define their permissions. 



_To set up access control:_
1. **Enable Authentication**: Configure MongoDB to require authentication by starting the server with --auth or setting security.authorization to enabled in the configuration file.

```yaml
# mongod.conf
security:
  authorization: enabled
```

2. **Create Users**: Use the db.createUser method to create users with specific roles.
3. **Assign Roles**: Assign roles to users that define their permissions, such as `read`, `write`, or `admin` roles for specific databases or collections.
4. To create a `admin` user in `MongoDB`, it must be created in the `admin` database, not in other databases.
    - The `root` role is global and must be created in the `admin` database.
    - Always switch to the admin database first: `use admin`
    - The `roles` field must specify both the **role** and **database**.


_Show all users in the current database:_
```JavaScript
use admin
show users
db.getUsers()
```


```JavaScript
use admin
db.createUser({
    user: "admin",
    pwd: "password",
    roles: [{ role: "root", db: "admin" }]
})


//Or:
db.createUser({
  user: "admin2",
  pwd: "password",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
});



//Or:
use db1

db.createUser({
  user: "dbuser",
  pwd: "password",
  roles: [{ role: "dbOwner", db: "db1" }]
});
```


_Log in using the newly created user:_
```bash
mongosh -u admin -p --authenticationDatabase admin
mongosh -u admin2 -p --authenticationDatabase admin
mongosh -u admin2 -p password --authenticationDatabase admin

mongosh -u dbuser -p --authenticationDatabase db1
mongosh -u dbuser -p password --authenticationDatabase db1
```


_MongoDB shell to authenticate:_
```JavaScript
db.auth("admin", "password")
db.auth("dbuser", "password")
```





### What is the aggregation framework in MongoDB?

The aggregation framework allows you to perform complex data processing pipelines involving filtering, grouping, sorting, and calculations.


### What are some common stages used in the aggregation framework?

Common stages include $match for filtering, `$group` for grouping documents, `$project` for selecting/excluding fields,` $sort` for sorting, etc.


### What is Embedding and Referencing?

#### Embedding:
Embedding means storing related data as nested documents or arrays within a parent document.
- Store related data inside the **same document**.
- One-to-many where the "many" are viewed with the parent
- Improved read performance (single read operation)
- Atomic writes for the entire document
- No joins needed

#### Referencing
Referencing means storing related data in separate documents and linking them through an identifier.
- Store related data in **separate documents** and connect them using an identifier, such as `_id`.
- Data has many-to-many relationships




### How do you troubleshoot a slow MongoDB query?
1. Run `db.collectionName.explain("executionStats").find({ field: "value" })`

```JavaScript
db.myCollection.explain("executionStats").find({ age: 31 })
db.myCollection.explain("executionStats").find({ name: "Alice" })
```

2. Check `COLLSCAN`, `IXSCAN`, and documents examined.
3. Verify whether the compound index matches the query and sort.
4. Review the profiler and slow-query logs.
5. Check CPU, RAM, disk I/O, cache pressure, and network latency.
6. Compare query latency before and after a controlled change.




---
---

