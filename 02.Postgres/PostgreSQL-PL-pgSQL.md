## PostgreSQL PL/pgSQL:

PL/pgSQL procedural language is similar to the Oracle PL/SQL. 

- PL/pgSQL is easy to learn and simple to use.
- PL/pgSQL comes with PostgreSQL by default. The user-defined functions and stored - procedures developed in PL/pgSQL can be used like any built-in functions and stored procedures.
- PL/pgSQL inherits all user-defined types, functions, and operators.
- PL/pgSQL has many features that allow you to develop complex functions and stored procedures.
- PL/pgSQL can be defined to be trusted by the PostgreSQL database server.



_PL/pgSQL has the following key features:_
- **SQL integration**: PL/pgSQL can execute SQL statements seamlessly within its code.
- **Block structure**: PL/pgSQL offers a block structure that organizes the code into blocks, making it easier to develop.
- **Control structures**: PL/pgSQL support conditionals and loops.
- **Error handling**: PL/pgSQL provides a robust error-handling mechanism.
- **Dynamic SQL**: PL/pgSQL can construct SQL queries flexibly and execute them dynamically.



### What is PL/pgSQL?
**PL/pgSQL (Procedural Language/PostgreSQL)** is PostgreSQL's built-in procedural programming language. It allows DBAs and developers to execute complex database operations, business logic, and automation directly inside PostgreSQL.

It extends standard SQL by adding programming features such as:
- Variables and constants
- IF-ELSE conditions
- LOOP, WHILE and FOR loops
- Exception handling
- Cursors
- Functions and procedures
- Records and arrays
- Dynamic SQL


### SQL vs. PL/pgSQL:

| SQL | PL/pgSQL |
| --- | -------- |
| Declarative language	| Procedural language |
| Executes individual SQL statements	| Executes a block of statements |
| No local variables in ordinary SQL statements	| Supports variables |
| No traditional IF-ELSE	| Supports IF-ELSE |
| No procedural loops	| Supports FOR, WHILE, LOOP |
| Used for CRUD operations	| Used for complex business logic |


---
---



## Basic PL/pgSQL Syntax:

_Each block has two sections:_
- **Declaration**: The declaration section is optional. It is where you declare variables, constants, and cursors.
- **Body**: The body section is required. It is where you put the logic of the block, such as SQL statements.


A block may have an optional `label` that is located at the beginning and end of the block. A block ends with a semicolon (`;`) after the `end` keyword.



_Basic Block Structure:_
```sql
[ <<label>> ]
[ DECLARE 
    -- Variable declarations go here
]
BEGIN
    -- Procedural statements and SQL queries go here
END [ label ];
```


### Anonymous Blocks (`DO`):

If you want to run PL/pgSQL code on the fly **without saving a reusable function**, you can wrap it in a `DO` statement using dollar-quoting (`$$`).


_Example-1: The basic structure of a PL/pgSQL block:_
```sql
DO $$
DECLARE
    -- Variable declaration
    v_name VARCHAR(100);
    v_salary NUMERIC;
BEGIN
    -- Executable statements
    v_name := 'AAA';
    v_salary := 50000;

    RAISE NOTICE 'Name: % and Salary: %', v_name, v_salary;
END;
$$ LANGUAGE plpgsql;
```


_Output:_
```
NOTICE:  Name: AAA and Salary: 50000
```


_Example-2:_
```sql
DO $$
DECLARE
    counter INTEGER := 10;
    message TEXT := 'The current count is: ';
BEGIN
    counter := counter + 5;
    RAISE NOTICE '% %', message, counter; 
END $$;
```


_Output:_
```
NOTICE:  The current count is:  15
```


_Example-3:_
```sql
DO $$
DECLARE
    v_id INT := 101;
    v_name VARCHAR(100) := 'BBB';
    v_salary NUMERIC(10,2) := 45000.50;
    v_active BOOLEAN := TRUE;
BEGIN
    RAISE NOTICE 'ID: %', v_id;
    RAISE NOTICE 'Name: %', v_name;
    RAISE NOTICE 'Salary: %', v_salary;
    RAISE NOTICE 'Active: %', v_active;
END;
$$;
```


_Output:_
```
NOTICE:  ID: 101
NOTICE:  Name: BBB
NOTICE:  Salary: 45000.50
NOTICE:  Active: t
```


### PL/pgSQL `SELECT INTO` Statement:

The `SELECT INTO` statement retrieves data from a table and assigns it to a variable:
```
SELECT column1, column2, ...
INTO variable1, variable2, ...
FROM table_name;
```

_In this syntax:_
- First, provide one or more columns of the table_name to retrieve data in the `SELECT` clause.
- Second, specify a variable list in the `INTO` clause.
- Third, specify the table name from which you retrieve data in the `FROM` clause.


_Example-4:_
```sql
do $$
<<first_block>>
declare
  user_id integer := 0;
begin
   -- get the number of users
   select count(*)
   into user_id
   from users;

   -- display a message
   raise notice 'The number of films is %', user_id;
end first_block $$;
```


_Output:_
```
NOTICE:  The number of films is 1000000
```


_Example-5:_
```sql
DO
$$
DECLARE
    v_username VARCHAR(100); -- Does not assign an initial value
BEGIN
    SELECT username 
    INTO v_username
    FROM users
    WHERE user_id = 1001;

    RAISE NOTICE 'The Username is %', v_username;
END;
$$;
```


_Output:_
```
NOTICE:  The Username is user_1001
```





>  `%` acts as a placeholder that gets replaced by the variables sequentially.



_Explanation:_
- `DO` : Executes an anonymous PL/pgSQL block.
- `DECLARE` : Declares variables.
- `BEGIN` : Starts executable statements.
- `:=` : Assigns values to variables.
- `RAISE NOTICE` : Displays messages.
- `END` : Ends the block.



---
---



## IF-ELSE Conditions:

```sql
DO $$
DECLARE
    v_salary NUMERIC := 60000;
BEGIN
    IF v_salary >= 50000 THEN
        RAISE NOTICE 'High Salary';

    ELSIF v_salary >= 30000 THEN
        RAISE NOTICE 'Medium Salary';

    ELSE
        RAISE NOTICE 'Low Salary';
    END IF;
END;
$$;
```

_Output:_
```
NOTICE:  High Salary
```


---
---



## LOOP Examples:


### Basic LOOP:

```sql
DO $$
DECLARE
    v_counter INTEGER := 1;
BEGIN
    LOOP
        RAISE NOTICE 'Counter: %', v_counter;

        v_counter := v_counter + 1;

        EXIT WHEN v_counter > 5;
    END LOOP;
END;
$$;
```


_Output:_
```
NOTICE:  Counter: 1
NOTICE:  Counter: 2
NOTICE:  Counter: 3
NOTICE:  Counter: 4
NOTICE:  Counter: 5
```


### WHILE LOOP:

```sql
DO $$
DECLARE
    v_counter INTEGER := 1;
BEGIN
    WHILE v_counter <= 5 LOOP
        RAISE NOTICE 'Counter: %', v_counter;

        v_counter := v_counter + 1;
    END LOOP;
END;
$$;
```


_Output:_
```
NOTICE:  Counter: 1
NOTICE:  Counter: 2
NOTICE:  Counter: 3
NOTICE:  Counter: 4
NOTICE:  Counter: 5
```



### FOR LOOP:

```sql
DO $$
DECLARE
    i INTEGER;
BEGIN
    FOR i IN 1..5 LOOP
        RAISE NOTICE 'Number: %', i;
    END LOOP;
END;
$$;
```


_Output:_
```
NOTICE:  Number: 1
NOTICE:  Number: 2
NOTICE:  Number: 3
NOTICE:  Number: 4
NOTICE:  Number: 5
```


---
---


## PL/pgSQL Functions:

A function is a reusable database object that can accept parameters and return a value or a result set.

A PL/pgSQL Function is a reusable database object that contains SQL statements and procedural logic. It allows you to execute complex database operations, perform calculations, validate data, and automate tasks inside PostgreSQL.

Functions can accept input parameters, process data, and return values or result sets.


_Common DBA use cases:_
- Retrieve records from tables.
- Insert, update, and delete data.
- Perform calculations.
- Validate user input.
- Generate reports.
- Implement business logic.
- Automate database operations.


_Basic Function Syntax:_
```sql
CREATE OR REPLACE FUNCTION function_name(
    parameter_name DATA_TYPE
)

RETURNS return_data_type
LANGUAGE plpgsql
AS $$

DECLARE
    -- Variable declarations
BEGIN
    -- SQL statements
    -- Procedural logic

    RETURN value;
END;
$$;
```


_Function Without Parameters:_
```sql
CREATE OR REPLACE FUNCTION welcome_message()
RETURNS TEXT
LANGUAGE plpgsql
AS $$

BEGIN
    RETURN 'Welcome to PostgreSQL PL/pgSQL';
END;
$$;
```


_Execute:_
```
SELECT welcome_message();
```



_Create a function:_
```sql
CREATE OR REPLACE FUNCTION get_user(
    p_user_id INTEGER
)

RETURNS VARCHAR
LANGUAGE plpgsql
AS $$

DECLARE
    v_user VARCHAR(50);
BEGIN
    SELECT username
    INTO v_user
    FROM users
    WHERE user_id = p_user_id;

    RETURN v_user;
END;
$$;
```


_Execute:_
```sql
SELECT get_user(101);
```



_Output:_
```
get_user
----------
 user_101
(1 row)
```


---
---


## Stored Procedures:

A PostgreSQL Stored Procedure is a reusable database object that contains SQL statements and procedural logic. It allows DBAs and developers to execute multiple database operations as a single unit.

Procedures are created using `CREATE PROCEDURE` and executed using the CALL statement.

_Common DBA use cases:_
- Database maintenance and automation.
- Insert, update, and delete operations.
- Data migration.
- Bulk data processing.
- Backup metadata management.
- Archiving old records.
- Transaction management.
- Database administration tasks.


_Basic Procedure Syntax:_
```sql
CREATE OR REPLACE PROCEDURE procedure_name(
    parameter_name DATA_TYPE
)
LANGUAGE plpgsql
AS $$
DECLARE
    -- Variable declarations
BEGIN
    -- SQL statements
    -- Procedural logic
END;
$$;
```



_Simple Procedure Without Parameters:_
```sql
CREATE OR REPLACE PROCEDURE welcome_getting()
LANGUAGE plpgsql
AS $$
BEGIN
    RAISE NOTICE 'Welcome to PostgreSQL Procedures';
END;
$$;
```


_Execute:_
```
CALL welcome_getting();
```



### Functions vs Procedures:


Both Functions and Procedures are reusable database objects in PostgreSQL. They allow DBAs and developers to execute SQL statements and procedural logic using PL/pgSQL.


_Key Differences:_
| Feature	| Function	| Procedure | 
| -------	| -------	| --------- | 
| Creation	| `CREATE FUNCTION`	| `CREATE PROCEDURE` | 
| Execution	| `SELECT`	| `CALL` |
| Return value	| Requires a return type (`RETURNS`) |	No return type required | 
| Return data	| Scalar, composite, SETOF, TABLE |	OUT/INOUT parameters |
| Parameters	| IN, OUT, INOUT |	IN, OUT, INOUT | 
| INSERT	| Supported	| Supported |
| UPDATE	| Supported	| Supported |
| DELETE	| Supported	| Supported |
| COMMIT	| Cannot commit its own transaction	| Supported in permitted contexts | 
| ROLLBACK	| Cannot roll back its own transaction |	Supported in permitted contexts |
| SQL expression	| Can be used in SELECT expressions |	Cannot be used as an expression |
| Main purpose	| Calculate and return data	| Execute database operations |



### Which command executes a PostgreSQL function?

SELECT


### Which command executes a PostgreSQL procedure?

CALL 


### Can a function execute COMMIT to end its own transaction?

No


### Can a function execute COMMIT or ROLLBACK?

No. A function cannot independently control its transaction using `COMMIT` or `ROLLBACK`.



### Can a procedure return values?

Yes. Procedures can return values using `OUT` and `INOUT` parameters.





---
---




**In-short:**   
"PostgreSQL functions and procedures are both reusable database objects. Functions are primarily used to return values or result sets and are invoked using `SELECT`. Procedures are primarily used to perform database operations and are invoked using `CALL`. 

The major difference is that procedures support transaction control, such as COMMIT and ROLLBACK, in permitted execution contexts, whereas functions do not."


---
---

