## SQL Data Types: 

SQL data types define the exact kind of value a table column can hold, such as integers, dates, text, or binary data. Selecting the correct data type is critical for **ensuring data integrity, optimizing query performance, and saving memory storage space**.

While SQL has an **ANSI standard** framework, slight variations in name and size parameters exist across popular relational database engines like MySQL, PostgreSQL, Microsoft SQL Server, and Oracle.


## MySQL Data Types:


Most commonly used in real applications:
- INT
- BIGINT
- DECIMAL(10,2)
- VARCHAR(255)
- TEXT
- BOOLEAN
- DATE
- DATETIME
- TIMESTAMP
- JSON




MySQL data types are generally divided into 5 major categories:

### 1. Numeric Data Types:

| Data Type | Description | Example |
|---|---|---|
| `TINYINT` | Very small integer | `TINYINT` |
| `SMALLINT` | Small integer | `SMALLINT` |
| `MEDIUMINT` | Medium integer | `MEDIUMINT` |
| `INT` / `INTEGER` | Standard integer | `INT` |
| `BIGINT` | Large integer | `BIGINT` |
| `DECIMAL` / `NUMERIC` | Exact decimal number | `DECIMAL(10,2)` |
| `FLOAT` | Single-precision floating point | `FLOAT` |
| `DOUBLE` / `REAL` | Double-precision floating point | `DOUBLE` |
| `BIT` | Bit-value type | `BIT(8)` |


### 2. String / Character Data Types:

| Data Type | Description | Example |
|---|---|---|
| `CHAR` | Fixed-length string | `CHAR(10)` |
| `VARCHAR` | Variable-length string | `VARCHAR(255)` |
| `TINYTEXT` | Small text | `TINYTEXT` |
| `TEXT` | Normal text | `TEXT` |
| `MEDIUMTEXT` | Medium text | `MEDIUMTEXT` |
| `LONGTEXT` | Very large text | `LONGTEXT` |
| `BINARY` | Fixed-length binary | `BINARY(16)` |
| `VARBINARY` | Variable-length binary | `VARBINARY(255)` |
| `TINYBLOB` | Small binary data | `TINYBLOB` |
| `BLOB` | Binary data | `BLOB` |
| `MEDIUMBLOB` | Medium binary data | `MEDIUMBLOB` |
| `LONGBLOB` | Large binary data | `LONGBLOB` |
| `ENUM` | One value from predefined list | `ENUM('Y','N')` |
| `SET` | Zero or more values from predefined list | `SET('A','B','C')` |


### 3. Date & Time Data Types:

| Data Type | Description | Example |
|---|---|---|
| `DATE` | Date only | `'2026-09-13'` |
| `TIME` | Time only | `'14:30:00'` |
| `DATETIME` | Date + time | `'2026-09-13 14:30:00'` |
| `TIMESTAMP` | Date + time, timestamp-oriented | `'2026-09-13 14:30:00'` |
| `YEAR` | Year | `2026` |


### 4. Spatial Data Types:

MySQL supports GIS/spatial data types:
| Data Type | Description |
|---|---|
| `GEOMETRY` | Generic geometric value |
| `POINT` | Single coordinate |
| `LINESTRING` | Line |
| `POLYGON` | Polygon |
| `MULTIPOINT` | Multiple points |
| `MULTILINESTRING` | Multiple lines |
| `MULTIPOLYGON` | Multiple polygons |
| `GEOMETRYCOLLECTION` | Collection of geometries |



### 5. JSON Data Type:

| Data Type | Description |
|---|---|
| `JSON` | Stores JSON documents |



---
---


## PostgreSQL Data Types:

PostgreSQL has a much richer type system than MySQL. The main categories are numeric, character, date/time, Boolean, binary, UUID, JSON, arrays, ranges, geometric, network, full-text search, XML, and user-defined types.

For a typical PostgreSQL + Java/Node.js/Python application, you'll use these most:

- BIGINT
- INTEGER
- NUMERIC(12,2)
- VARCHAR(255)
- TEXT
- BOOLEAN
- DATE
- TIMESTAMP
- TIMESTAMPTZ
- INTERVAL
- UUID
- JSONB
- BYTEA
- TEXT[]
- INTEGER[]
- INET
- CIDR


#### 1. Numeric Data Types:

| Data Type | Description | Example |
|---|---|---|
| `smallint` | 2-byte integer | `smallint` |
| `integer` / `int` | 4-byte integer | `integer` |
| `bigint` | 8-byte integer | `bigint` |
| `decimal` / `numeric` | Exact decimal | `numeric(10,2)` |
| `real` | 4-byte floating point | `real` |
| `double precision` | 8-byte floating point | `double precision` |
| `smallserial` | Auto-incrementing 2-byte integer | `smallserial` |
| `serial` | Auto-incrementing 4-byte integer | `serial` |
| `bigserial` | Auto-incrementing 8-byte integer | `bigserial` |



#### 2. Character / String Data Types:

| Data Type | Description | Example |
|---|---|---|
| `character(n)` / `char(n)` | Fixed-length string | `char(10)` |
| `character varying(n)` / `varchar(n)` | Variable-length string | `varchar(255)` |
| `text` | Unlimited-length text | `text` |


#### 3. Boolean:

| Data Type | Values |
|---|---|
| `boolean` / `bool` | `TRUE`, `FALSE`, `NULL` |



#### 4. Date & Time:

| Data Type | Description |
|---|---|
| `date` | Date |
| `time` | Time without timezone |
| `time with time zone` | Time with timezone |
| `timestamp` | Date + time without timezone |
| `timestamp with time zone` / `timestamptz` | Date + time with timezone |
| `interval` | Time interval |




#### 5. UUID:

UUID is particularly useful for distributed applications.

PostgreSQL has native UUID support: `id UUID`

_Example:_
```
CREATE TABLE users (
    id UUID PRIMARY KEY,
    name VARCHAR(100)
);
```

#### 6. JSON:

| Data Type | Description |
|---|---|
| `json` | JSON data |
| `jsonb` | Binary/decomposed JSON, usually preferred for querying |



#### 7. Binary Data:

| Data Type | Description |
|---|---|
| `bytea` | Binary data |



#### 8. Arrays:
PostgreSQL supports arrays of almost any built-in or user-defined type.

```
INTEGER[]
TEXT[]
VARCHAR(100)[]
UUID[]
```

_Example:_
```
CREATE TABLE employees (
    id BIGINT,
    skills TEXT[]
);
```



#### 9. Network Address Types:

Very useful for infrastructure, networking, and security applications.

| Data Type | Description |
|---|---|
| `inet` | IPv4/IPv6 host or network |
| `cidr` | IPv4/IPv6 network |
| `macaddr` | MAC address |
| `macaddr8` | EUI-64 MAC address |



#### 10. Geometric Types:

PostgreSQL has built-in geometric types.

| Data Type | Description |
|---|---|
| `point` | Point |
| `line` | Infinite line |
| `lseg` | Line segment |
| `box` | Rectangle |
| `path` | Geometric path |
| `polygon` | Polygon |
| `circle` | Circle |

#### 11. Full-Text Search Types:

| Data Type | Description |
|---|---|
| `tsvector` | Processed searchable document |
| `tsquery` | Full-text search query |




#### 12. PostgreSQL-Specific / Special Types:

| Type | Purpose |
|---|---|
| `pg_lsn` | PostgreSQL Log Sequence Number |
| `txid_snapshot` | Transaction ID snapshot |
| `pg_snapshot` | Transaction snapshot |
| `tid` | Tuple identifier |
| `xid` | Transaction ID |
| `xid8` | 64-bit transaction ID |


---
---



## Oracle Database Data Types:


This reference covers common SQL types, PL/SQL types, and specialized Oracle types.

_Commonly Used Oracle Data Types:_
| Use Case | Recommended Data Type |
|---|---|
| Employee ID | `NUMBER(10)` |
| Financial amount | `NUMBER(12,2)` |
| Employee name | `VARCHAR2(100)` |
| Country code | `CHAR(2)` |
| National-language name | `NVARCHAR2(100)` |
| Birth date | `DATE` |
| Event timestamp | `TIMESTAMP(6)` |
| Timestamp with timezone | `TIMESTAMP WITH TIME ZONE` |
| Duration | `INTERVAL DAY TO SECOND` |
| Large text document | `CLOB` |
| Binary document | `BLOB` |
| External file reference | `BFILE` |
| Binary identifier | `RAW(16)` |
| JSON in Oracle 19c | `CLOB` with `IS JSON` validation |
| Native JSON in Oracle 21c+ | `JSON`, where supported |
| XML document | `XMLTYPE` |
| Spatial coordinates | `SDO_GEOMETRY`, where available |
| Row locator | `ROWID` |



### 1. Numeric Data Types:

| Data Type | Description | Example |
|---|---|---|
| NUMBER | Variable-precision numeric value | `NUMBER` |
| NUMBER(p) | Number with specified precision | `NUMBER(10)` |
| NUMBER(p,s) | Number with precision and scale | `NUMBER(10,2)` |
| DECIMAL(p,s) | Synonym-style numeric declaration | `DECIMAL(10,2)` |
| DEC(p,s) | Alternative declaration for decimal numeric | `DEC(8,2)` |
| NUMERIC(p,s) | Numeric declaration | `NUMERIC(10,2)` |
| INTEGER | Integer numeric subtype | `INTEGER` |
| INT | Integer numeric subtype | `INT` |
| SMALLINT | Integer numeric subtype | `SMALLINT` |
| FLOAT(p) | Floating-point number specified using binary precision | `FLOAT(126)` |
| REAL | Floating-point numeric subtype | `REAL` |
| DOUBLE PRECISION | Floating-point numeric subtype | `DOUBLE PRECISION` |
| BINARY_FLOAT | 32-bit binary floating-point number | `BINARY_FLOAT` |
| BINARY_DOUBLE | 64-bit binary floating-point number | `BINARY_DOUBLE` |



### 2. Character and String Data Types:

| Data Type | Description | Example |
|---|---|---|
| CHAR(n) | Fixed-length character string | `CHAR(10)` |
| VARCHAR2(n) | Variable-length character string | `VARCHAR2(255)` |
| NCHAR(n) | Fixed-length national character string | `NCHAR(20)` |
| NVARCHAR2(n) | Variable-length national character string | `NVARCHAR2(100)` |
| LONG | Legacy variable-length character data | `LONG` |



### 3. Date and Time Data Types:

| Data Type | Description | Example |
|---|---|---|
| DATE | Date and time to whole-second precision | `DATE` |
| TIMESTAMP(p) | Date and time with fractional seconds | `TIMESTAMP(6)` |
| TIMESTAMP WITH TIME ZONE | Timestamp with timezone information | `TIMESTAMP(6) WITH TIME ZONE` |
| TIMESTAMP WITH LOCAL TIME ZONE | Timestamp normalized to the database timezone and displayed in the session timezone | `TIMESTAMP(6) WITH LOCAL TIME ZONE` |
| INTERVAL YEAR(p) TO MONTH | Duration in years and months | `INTERVAL YEAR(2) TO MONTH` |
| INTERVAL DAY(p) TO SECOND(s) | Duration in days and time units | `INTERVAL DAY(3) TO SECOND(6)` |



### 4. Binary Data Types:

| Data Type | Description | Example |
|---|---|---|
| RAW(n) | Variable-length binary data | `RAW(32)` |
| LONG RAW | Legacy variable-length binary data | `LONG RAW` |



### 5. Large Object (LOB) Data Types:

| Data Type | Description | Example |
|---|---|---|
| CLOB | Large character data | `CLOB` |
| NCLOB | Large national character data | `NCLOB` |
| BLOB | Large binary data | `BLOB` |
| BFILE | Read-only reference to an external binary file | `BFILE` |



### 6. Row Identifier Data Types:

| Data Type | Description | Example |
|---|---|---|
| ROWID | Physical row locator | `ROWID` |
| UROWID | Universal row identifier, including logical row identifiers | `UROWID` |



### 7. JSON Data Types and Storage:

| Type / Option | Description | Availability |
|---|---|---|
| VARCHAR2 with IS JSON constraint | JSON text with validation | Oracle 12c and later, subject to release |
| CLOB with IS JSON constraint | Large JSON text with validation | Oracle 12c and later, subject to release |
| BLOB with IS JSON constraint | Binary-stored JSON text with validation | Oracle 12c and later, subject to release |
| JSON | Native JSON SQL data type | Oracle Database 21c and later releases that support it |


### 8. XML Data Type:

| Data Type | Description | Example |
|---|---|---|
| XMLTYPE | Stores and processes XML documents | `XMLTYPE` |



### 9. Spatial and Geometric Data Types:

| Data Type | Description | Availability |
|---|---|---|
| SDO_GEOMETRY | Geometric and spatial data | Oracle Spatial |
| SDO_TOPO_GEOMETRY | Topological geometry | Oracle Spatial |
| SDO_GEORASTER | Georeferenced raster data | Oracle GeoRaster |



### 10. Object and User-Defined Data Types:

| Type | Description | Example |
|---|---|---|
| Object type | User-defined structured type with attributes and optional methods | `address_type` |
| REF | Reference to an object-table row | `REF address_type` |



### 11. Collection Types:

| Type | Description | Usage |
|---|---|---|
| VARRAY | Ordered collection with a declared maximum size | SQL and PL/SQL |
| Nested table | Collection of elements that can be stored in a table column | SQL and PL/SQL |
| Associative array | Key-indexed collection | PL/SQL |



## 12. PL/SQL Numeric Types:

| Data Type | Description |
|---|---|
| PLS_INTEGER | Signed PL/SQL integer |
| BINARY_INTEGER | Signed PL/SQL integer |
| SIMPLE_INTEGER | Non-null PLS_INTEGER subtype |
| NATURAL | Nonnegative PLS_INTEGER subtype |
| NATURALN | Non-null NATURAL subtype |
| POSITIVE | Positive PLS_INTEGER subtype |
| POSITIVEN | Non-null POSITIVE subtype |
| SIGNTYPE | Integer subtype representing -1, 0, or 1 |

> These are PL/SQL types or subtypes, not generally declared as ordinary SQL table-column types.



## 13. PL/SQL Character and Boolean Types:

| Data Type | Description |
|---|---|
| BOOLEAN | Logical TRUE, FALSE, or NULL |
| CHAR | Fixed-length character data |
| VARCHAR2 | Variable-length character data |
| NCHAR | Fixed-length national character data |
| NVARCHAR2 | Variable-length national character data |
| LONG | Legacy character data |

> SQL support for `BOOLEAN` depends on the Oracle Database version. SQL `BOOLEAN` columns are supported in Oracle Database 23ai and later releases that include the feature; older releases generally restrict `BOOLEAN` to PL/SQL.




### 14. Object Identifier and Catalog Types:

| Data Type | Description |
|---|---|
| REF | Object reference |
| ROWID | Physical row identifier |
| UROWID | Universal row identifier |

Oracle also uses internal identifier types in its data dictionary and system interfaces. These should not be confused with a universal set of application-column types.



### 15. Advanced Oracle-Supplied Types:

| Data Type | Description |
|---|---|
| ANYTYPE | Describes a data type dynamically |
| ANYDATA | Stores a value together with its type information |
| ANYDATASET | Represents a set of values with type information |
| URIType | Abstract URI-related type |
| HTTPURITYPE | HTTP URI-related type |
| DBURITYPE | Database URI-related type |
| XDBURITYPE | Oracle XML DB URI-related type |

> Availability of advanced Oracle-supplied types can depend on database release, installed components, and privileges.



### 16. Deprecated or Legacy Types:

| Data Type | Description | Recommendation |
|---|---|---|
| LONG | Legacy large character data | Prefer CLOB |
| LONG RAW | Legacy large binary data | Prefer BLOB |



---
---

