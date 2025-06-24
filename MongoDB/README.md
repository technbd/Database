
## MongoDB:


### Database Management:

#### Show all databases:
```
show dbs
```


#### Create new or switch to a database:
```
use <dbname>
use mydb1
```


#### Show current database:
```
db
```


#### Total document count:
```
use <dbname>
show collections


db.<collection_name>.count();

db.notifications.count();
db.startup_log.count();

or,

db.<collection_name>.countDocuments();

db.notifications.countDocuments();
db.startup_log.countDocuments();
```


#### Check database stats:
```
db.stats()
```


#### Drop database:
```
use mydb3
db.dropDatabase()
```


### User Management:

By default, MongoDB allows access without authentication. Enable authentication in the MongoDB config file (usually `/etc/mongod.conf`): 

```
vim /etc/mongod.conf

security:
  authorization: enabled
```


```
systemctl restart mongod
```



#### Create user:
To create a root user in MongoDB, it must be created in the admin database, not in other databases.
- The `root` role is global and must be created in the `admin` database.
- Always switch to the `admin` database first: `use admin`
- The `roles` field must specify both the **role** and **database**.


_Database-Specific Roles:_
- role: "root" : Superuser: Full access to everything in the MongoDB instance (full access to all databases).
- role: "readWrite" : allows the user to insert, update, and delete documents.
- role: "read" : Read-only access to a database
- role: "dbAdmin" : Administrative tasks (indexes, stats, users) but cannot read/write data 
- role: "userAdmin" : Manage users and roles in a database
- role: "dbOwner" : Full control over the database (combines all roles above).

- role: "readAnyDatabase" :	Read access to all databases.
- role: "readWriteAnyDatabase" :	Read/write access to all databases.

- role: "backup" :	Allows running backup-related commands.
- role: "restore" :	Allows running restore-related commands.


_Create `admin` user:_
```
use admin
```


```
db.createUser({
    user: "root",
    pwd: "secret",
    roles: [ { role: "root", db: "admin" } ]
})
```



_Log in using the newly created user:_
```
mongosh -u root -p --authenticationDatabase <database>

mongosh -u root -p --authenticationDatabase admin
mongosh -u root -p <pwd> --authenticationDatabase admin
```



_To create a user for a specific database:_

```
use mydb1
```


```
db.createUser({
  user: "user1",
  pwd: "dbpass",
  roles: [{ role: "readWrite", db: "mydb1" }]
})
```



```
use mydb2

db.createUser({
  user: "user2",
  pwd: "pass234",
  roles: [
    { role: "read", db: "mydb1" },
    { role: "readWrite", db: "mydb2" },
    { role: "backup", db: "admin" }
  ]
})
```


```
mongosh -u user1 -p dbpass --authenticationDatabase mydb1
```


#### Update User Password:
```
use mydb1

db.updateUser("user1", { pwd: "newpass" })
```



#### Show users:
```
use mydb2

show users
db.getUsers()
```


#### Drop user:
```
db.dropUser("username")
db.dropUser("user1")
```




### Database Backup:

If you need to backup & restore entire databases:
- `mongodump` : Creates a binary backup of the database
- `mongorestore` : Restores a database from a `mongodump` backup


```
mongodump --db <myDatabase> --out /backup/path/

mongodump --db mydb1 --out /home/uistl0/
```


### Database Restore:
```
mongorestore --db <myDatabase> /backup/path/myDatabase

mongorestore --db mydb1 /home/uistl0/mydb1
```









