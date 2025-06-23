## PostgreSQL:


### Database Management:: 

#### Create a new database:

```
CREATE DATABASE db1;

CREATE DATABASE db1 OWNER myuser;
```



#### List databases:
```
\l
```


#### Connect to a database:
```
\c <db_name>
\c db2
```



#### Create Table:
```
CREATE TABLE t1 (id INT PRIMARY KEY NOT NULL, name CHAR(20)); 

INSERT INTO t1 (id, name) VALUES (1, 'Jaber');

SELECT * FROM t1; 
```


#### List tables:
```
\dt

        List of relations
 Schema | Name | Type  |  Owner
--------+------+-------+----------
 public | t1   | table | postgres
```


#### Describe a table: 
```
\d <table_name>
\d t1
```



#### Drop Table:
```
DROP TABLE t1;
```


#### Drop Database:
```
DROP DATABASE db2;
```


#### SHOW Commands:
```
show data_directory;
show config_file;
show hba_file;
show log_filename;
```


---
---




### User Management:


#### Create User and Database:

_Best: Method-1_
```
psql -U postgres
```


```
select current_user;

 current_user
--------------
 postgres
```


```
SELECT current_database();

 current_database
------------------
 postgres
```


_Syntax:_
```
CREATE USER [username] WITH PASSWORD 'password';
```


_Create a New User:_
```
create user user1 with encrypted password 'user123';
create user user2 with encrypted password 'user234';
create user user3 with encrypted password 'user345';
```


_Change a User’s Password:_
```
alter user user2 with password 'user23456';
```


```
create database db2 owner user2;
```


```
\l

Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 db1       | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 db2       | user2    | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
```


_Database ownership change:_
```
alter database db1 owner to user1;
```


```
\l

                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 db1       | user1    | UTF8     | en_US.utf8 | en_US.utf8 |
 db2       | user2    | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
```



#### Grant privileges to a user: 

```
grant all privileges on database db2 to user3;
```



```
\l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 db1       | user1    | UTF8     | en_US.utf8 | en_US.utf8 |
 db2       | user2    | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/user2            +
           |          |          |            |            | user2=CTc/user2      +
           |          |          |            |            | user3=CTc/user2
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
```




#### Drop User:
```
drop user <username>;

drop user if exists rahim;

drop user if exists replicator;
```



---
---


### Create Role: 


#### Create REPLICATION User: 

```
create user replicator with replication encrypted password 'admin123';
```



_To list all roles (users/groups) in a PostgreSQL:_

```
\du

 List of roles
 Role name  |                         Attributes                         | Member of
------------+------------------------------------------------------------+-----------
 postgres   | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 replicator | Replication                                                | {}
 user1      |                                                            | {}
 user2      |                                                            | {}
 user3      |                                                            | {}
```



```
ALTER USER user1 REPLICATION;
```


```
\du

                                    List of roles
 Role name  |                         Attributes                         | Member of
------------+------------------------------------------------------------+-----------
 postgres   | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 replicator | Replication                                                | {}
 user1      | Replication                                                | {}
 user2      |                                                            | {}
 user3      |                                                            | {}
```



```
SELECT * FROM pg_roles;

          rolname          | rolsuper | rolinherit | rolcreaterole | rolcreatedb | rolcanlogin | rolreplication | rolconnlimit | rolpassword | rolvaliduntil | rolbypassrls | rolconfig |  oid
---------------------------+----------+------------+---------------+-------------+-------------+----------------+--------------+-------------+---------------+--------------+-----------+-------
 pg_signal_backend         | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  4200
 pg_read_server_files      | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  4569
 postgres                  | t        | t          | t             | t           | t           | t              |           -1 | ********    |               | t            |           |    10
 pg_write_server_files     | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  4570
 replicator                | f        | t          | f             | f           | t           | t              |           -1 | ********    |               | f            |           | 16394
 pg_execute_server_program | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  4571
 pg_read_all_stats         | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  3375
 user3                     | f        | t          | f             | f           | t           | f              |           -1 | ********    |               | f            |           | 16393
 pg_monitor                | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  3373
 user2                     | f        | t          | f             | f           | t           | f              |           -1 | ********    |               | f            |           | 16391
 user1                     | f        | t          | f             | f           | t           | t              |           -1 | ********    |               | f            |           | 16390
 pg_read_all_settings      | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  3374
 pg_stat_scan_tables       | f        | t          | f             | f           | f           | f              |           -1 | ********    |               | f            |           |  3377
(13 rows)
```



#### Grant role to user `zbx_monitor`: 
```
CREATE USER zbx_monitor WITH PASSWORD 'Admin@123' INHERIT;
```


```
GRANT <myrole> TO <myuser>;

GRANT pg_monitor TO zbx_monitor;
```


#### Basic Role with Login (User):
```
CREATE ROLE user4 WITH LOGIN PASSWORD 'mypassword';
```


#### Create Role with Privileges:
```
CREATE ROLE user4 WITH LOGIN CREATEDB CREATEROLE PASSWORD 'user4pass';
```


#### Create Superuser:
```
CREATE ROLE user5 WITH SUPERUSER LOGIN PASSWORD 'user5pass';
```


#### Read-Only Role (without login):
```
CREATE ROLE readonly;
CREATE ROLE readonly NOINHERIT;
```


```
GRANT readonly TO myuser;
```



```
\du

                                      List of roles
  Role name  |                         Attributes                         |  Member of
-------------+------------------------------------------------------------+--------------
 postgres    | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 readonly    | Cannot login                                               | {}
 replicator  | Replication                                                | {}
 user1       | Replication                                                | {}
 user2       |                                                            | {}
 user3       |                                                            | {}
 user4       | Create role, Create DB                                     | {}
 user5       | Superuser                                                  | {}
 zbx_monitor |                                                            | {pg_monitor}
```



#### Delete a Role:



---
---


### Create Tablespace:

_Create a directory on the filesystem:_
```
mkdir /mnt/db1_tablespaces
chown postgres:postgres /mnt/db1_tablespaces
```


_Create the tablespace in SQL:_
```
CREATE TABLESPACE db1_ts
  OWNER user1
  LOCATION '/mnt/db1_tablespaces';
```


_List all tablespaces:_
```
\db

             List of tablespaces
    Name    |  Owner   |       Location
------------+----------+----------------------
 db1_ts     | user1    | /mnt/db1_tablespaces
 pg_default | postgres |
 pg_global  | postgres |
```


Or,

```
SELECT spcname, pg_tablespace_location(oid) 
FROM pg_tablespace;
```


_Create a table using the tablespace:_
```
CREATE TABLE t1 (
    id SERIAL PRIMARY KEY,
    name CHAR(20) 
) TABLESPACE db1_ts;
```


```
INSERT INTO t1 (id, name) VALUES (1, 'Jaber');
SELECT * FROM t1; 
```




---
---



### Database Export/Backup:

- `-U` , --username=NAME :      connect as specified database user
- `-h` , --host=HOSTNAME :    database server host or socket directory
- `-d` , --dbname=DBNAME :     database to dump
- `-p` , --port=PORT     :     database server port number
- `-b` : Includes large objects in the backup.
- `-f` `backupfile.dump` : The name of the file where the custom-format backup will be saved.
- `-F` , --format=c|d|t|p :     output file format (custom, directory, tar, plain text (default))
- `-F c`: Custom format, Specifies the output format as custom.
- `-F d` : Specifies the output format as a directory.
- `-c` , --clean :            clean (drop) databases before recreating
- `--no-role-passwords` :         do not dump passwords for roles
- `-v` : Enables verbose mode, which provides more detailed output during the backup process.




#### Single database backup:
```
pg_dump -U postgres -d db1 > /home/db1_full_db.sql

or,

pg_dump -U postgres -d db1 -f /home/db1_full_db_bk.sql
```


#### Custom Format Backup:

_Custom Format Backup (for `pg_restore`):_
```
pg_dump -U postgres -d db1 -F c -f /home/db1_full_dump.dump
```





#### All database backup:
To back up all databases in a PostgreSQL cluster, you can use the `pg_dumpall` utility. The `pg_dumpall` utility automatically includes **roles and tablespaces** in the backup. However, you can explicitly specify this by using the `--roles-only` or `--tablespaces-only` options if you only want to back up those objects. A single SQL file containing all databases and includes roles, tables, schemas, and permissions. 

```
pg_dumpall -U postgres > /home/all_db_dump.sql

Or,

pg_dumpall -U postgres -f /home/all_db_dump_01.sql
```



#### Database specific table backup:
You must include the schema name (like `public.employees`) if the table is not in the search path.

- `-t` table, `--table=`table : Dump only tables (or views or sequences or foreign tables) matching table. 

```
pg_dump -U postgres -d db1 --table=t1 -f /home/db1_t1_table_bk.sql

pg_dump -U postgres -d db1 --table=public.t2 -f /home/db1_t2_table_bk.sql
```


_Backup Multiple Tables:_
```
pg_dump -U postgres -d db1 --table=public.t1 --table=public.t2 -f /home/db1_t1_t2_table_bk.sql
```


#### Database schema backup:

Backs up only the structure: tables, views, functions, sequences, etc.

- `-s`, `--schema-only` : Dump only the object definitions (schema), not data.


_Full schema backup:_
```
pg_dump -U postgres -d db1 --schema-only > /home/db1_schema_bk.sql
```


_Specific Table Schema Backup:_
```
pg_dump -U postgres -d db1 --table=public.t1 --schema-only -f /backups/db_t1_schema_bk.sql
```




### Database Restore:

#### Single database Restore:
```
psql -U postgres -d newdb1 < /home/db1_full_db.sql

or,

psql -U postgres -d newdb2 -f /home/db1_full_db_bk.sql
```


_Restore Custom Format:_
```
pg_restore -U postgres -d newdb3 /home/db1_full_dump.dump
```


#### Restore All Databases:
```
psql -U postgres < /home/all_db_dump.sql

Or,

psql -U postgres -f /home/all_db_dump_01.sql
```


#### Restore the Table:

```
psql -U postgres -d db1 -f /home/db1_t2_table_bk.sql

psql -U postgres -d db1 -f /home/db1_t1_t2_table_bk.sql
```




#### Database Schema Restore:

```
psql -U postgres -d db1 < /home/db1_schema_bk.sql
```


```
psql -U postgres -d db1 < /home/db_t1_schema_bk.sql
```




### Links:
- [pg_dump options](https://www.postgresql.org/docs/current/app-pgdump.html)








