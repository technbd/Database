## MySQL:


#### 1. MySQL Community Edition: 
MySQL Community Edition is the world's most popular open-source database that can be downloaded for free. Individuals and organizations can utilize it for a variety of purposes.

The Community Edition has several restrictions, including a lack of advanced features like backup and recovery, performance monitoring, and security advancements in the Enterprise Edition. You will not, however, receive official assistance from the MySQL development team. 


#### 2. MySQL Standard Edition:
MySQL Standard Edition is a paid version that provides extra analytics capabilities and support services. It contains all of MySQL's fundamental functionality and some extras like sophisticated backup and recovery, performance monitoring, and security upgrades.

This edition's cost is determined by the number of processors used, with discounts possible for more extensive deployments. MySQL Standard Edition costs different amounts based on the number of servers and cores. 

InnoDB is included in MySQL Standard Edition, making it a fully integrated transaction-safe, ACID-compliant database. Furthermore, MySQL Replication enables you to deliver high-performance, scalable web applications.


#### 3. MySQL Enterprise Edition:
MySQL Enterprise Edition provides additional features and support services such as high availability, security, and speed enhancements. MySQL Enterprise Edition costs different amounts based on the number of servers and cores. 

MySQL Enterprise Edition is appropriate for mission-critical applications requiring enhanced capabilities for high availability, security, and performance optimization. 





### Database Management:

#### Create Database:
```
create database db1;
```


#### Create Table: 
```
CREATE TABLE test1 (name VARCHAR(20));
INSERT INTO test1 (name) VALUES ('jaber');
```

```
CREATE TABLE test2 (name VARCHAR(20));
INSERT INTO test2 (name) VALUES ('karim');
```


```
show tables;

desc <table_name>;
describe <table_name>;
```


#### Drop Table:
```
drop table <table_name>;
```


#### Drop Linked Table:

```
set foreign_key_checks=0;

set foreign_key_checks=1;

show variables like "foreign_key%";
```


#### Drop Database:
```
drop database db2;
```




### User Management: 

#### Creating Users:
```
create user 'user1'@'%' identified by 'user1@123';

create user 'user2'@'localhost' IDENTIFIED WITH mysql_native_password BY 'user2@123';
```


```
SELECT user,host FROM mysql.user;
SELECT user,host,authentication_string,plugin FROM mysql.user;

select user, host, grant_priv, super_priv, drop_priv from mysql.user;
```


#### Granting privileges:
```
GRANT ALL ON *.* TO 'user1'@'%';

GRANT ALL PRIVILEGES ON *.* TO 'user2'@'localhost';

grant all privileges on db1.* to 'user2'@'localhost';

SHOW GRANTS FOR 'user2'@'localhost';
```




#### Update Users:
```
select user();

ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

UPDATE user set plugin="caching_sha2_password" where User='root';

FLUSH PRIVILEGES;
```



#### Drop Users:
```
DROP USER 'username'@'hostname';

DROP USER 'user1'@'%';
DROP USER 'user2'@'localhost';
```





### Database Backup:

#### Single database backup:

_Syntax:_
```
mysqldump -u <user_name> -p <database_name> > backup_name.sql
```


```
mysqldump -u root -p db1 > /home/db1_full_DB.sql
```


#### All database backup:
```
mysqldump -u root -p --all-databases > /home/all_databases_backup.sql
```


#### Database specific table backup::
```
mysqldump -u root -p db1 test1 > /home/test1_table_structure_with_data.sql

mysqldump -u root -p db1 test1 test2 > /home/test1_test2_table_structure_with_data.sql
```



#### Database schema backup:

_Full schema backup:_
```
mysqldump -u root -p --no-data db1 > /home/db1_schema_only.sql
```


_Orders schema backup:_
```
mysqldump -u root -p --no-data db1 test1 > /home/db1_test1_schema.sql

mysqldump -u root -p --no-data db1 orders > /home/db1_orders_schema.sql
```



### Database Restore:

#### Single Database restore:
```
create database db1;

mysql -u root -p db1 < /home/db1_full_DB.sql
```


Or,

```
mysql> create database db1;
mysql> use db1;

mysql> source /home/db1_full_DB.sql
mysql> show tables;
```


#### All Database restore:
```
mysql -u root -p < /home/all_databases_backup.sql
```


#### Restore a Specific Table:
```
mysql -u root -p db1 < /home/test1_table_structure_with_data.sql
```


Or,

```
use db1;

source /home/test1_table_structure_with_data.sql
```


#### Database Schema Restore:
```
create database db1;

mysql -u root -p db1 < /home/db1_schema_only.sql
```








