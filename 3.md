# Assignment No. - 3

## Title

SQL Queries for Data Manipulation, Access Control, and Transactions.

## Problem Statement

SQL Queries for Data Manipulation, Access Control, and Transactions.

Design and run SQL queries to demonstrate the following:

- Data Manipulation (DML): Use SQL statements to INSERT, UPDATE, and DELETE records. Apply arithmetic, logical, set operators, pattern matching, and string functions.
- Access Control DCL Language commands: Use GRANT, REVOKE, and ROLE commands to manage user access.
- Transaction Control (TCL): Apply START TRANSACTION, COMMIT, ROLLBACK, and SAVEPOINT commands to manage transactions.

## Objective

To understand the different issues involved in the design and implementation of a database system To understand and use data manipulation language to query, update, and manage a database.

## Theory

### a) DATA MANIPULATION LANGUAGE (DML)

The Data Manipulation Language (DML) is used to retrieve, insert and modify database information. These commands will be used by all database users during the routine operation of the database.

Let's take a brief look at the basic DML commands.

### 1. INSERT

### 2. UPDATE

### 3. DELETE

### 1. INSERT INTO

This is used to add records into a relation. These are three type of INSERT INTO queries which are as

### a) Inserting a single record

#### Syntax

```sql
INSERT INTO < relation/table name>

(field_1,field_2……field_n)VALUES (data_1,data_2,................................ data_n);
```

#### Example

```sql
SQL>INSERT INTO devices(device_id,device_code,device_name,current_status)VALUES

(101,'VX-ESP-01','VisionX Lab Glasses','IDLE');
```

### b) Inserting a single record

#### Syntax

```sql
INSERT INTO < relation/table name>VALUES (data_1,data_2,........ data_n);
```

#### Example

```sql
SQL>INSERT INTO session_events VALUES

(7001,501,'session.streaming','Streaming started',SYSDATE);
```

### c) Inserting all records from another relation

#### Syntax

```sql
INSERT INTO relation_name_1 SELECT

Field_1,field_2,field_n FROM relation_name_2 WHERE field_x=data;
```

#### Example

```sql
SQL>INSERT INTO session_archive SELECT

session_id,device_id FROM sessions WHERE session_state = 'COMPLETE';
```

### d) Inserting multiple records

#### Syntax

```sql
INSERT INTO relation_name field_1,field_2,..... field_n) VALUES

(&data_1,&data_2,........&data_n);
```

#### Example

```sql
SQL>INSERT INTO session_events (event_id, session_id,

event_type,event_message,created_at) VALUES (&event_id,'&session_id','&event_type','&event_message',SYSDATE); Enter value for event_id: 7001 Enter value for session_id: 501 Enter value for event_type: session.streaming Enter value for event_message: Streaming started
```

### 2. UPDATE-SET-WHERE

This is used to update the content of a record

in a relation.

#### Syntax

```sql
SQL>UPDATE relation name SET

Field_name1=data,field_name2=data, WHERE field_name=data;
```

#### Example

```sql
SQL>UPDATE analysis_jobs SET job_status = 'RUNNING' WHERE job_id = 9001;
```

### 3. DELETE-FROM

This is used to delete all the records of a

relation but it will retain the structure of that relation.

a) DELETE-FROM: This is used to delete all the records of relation.

#### Syntax

```sql
SQL>DELETE FROM relation_name;
```

#### Example

```sql
SQL> DELETE FROM session_events;
```

### b) DELETE -FROM-WHERE

This is used to delete a selected record

from a relation.

#### Syntax

```sql
SQL>DELETE FROM relation_name WHERE condition;
```

#### Example

```sql
SQL> DELETE FROM device_health_log WHERE health_log_id = 3002;
```

### ARIHMETIC OPERATORS

(+): Addition - Adds values on either side of the operator. (-):Subtraction - Subtracts right hand operand from left hand operand. (*):Multiplication - Multiplies values on either side of the operator. (/):Division - Divides left hand operand by right hand operand. (^):Power- raise to power of. (%):Modulus - Divides left hand operand by right hand operand and returns remainder.

### LOGICAL OPERATORS

AND: The AND operator allows the existence of multiple conditions in an SQL statement's WHERE clause. OR: The OR operator is used to combine multiple conditions in an SQL statement's WHERE clause. NOT: The NOT operator reverses the meaning of the logical operator with which it is used. Eg: NOT EXISTS, NOT BETWEEN, NOT IN, etc. This is a negate operator.

### COMPARISION OPERATORS

(=):Checks if the values of two operands are equal or not, if yes then condition becomes true. (!=):Checks if the values of two operands are equal or not, if values are not equal then condition becomes true. (< >):Checks if the values of two operands are equal or not, if values are not equal then condition becomes true. (>):Checks if the value of left operand is greater than the value of right operand, if yes then condition becomes true (<):Checks if the value of left operand is less than the value of right operand, if yes then condition becomes true. (>=):Checks if the value of left operand is greater than or equal to the value of right operand, if yes then condition becomes true. (<=):Checks if the value of left operand is less than or equal to the value of right operand, if yes then condition becomes true.

### PATTERN MATCHING

BETWEEN: The BETWEEN operator is used to search for values that are within a set of values, given the minimum value and the maximum value. IS NULL: The NULL operator is used to compare a value with a NULL attribute value. ALL: The ALL operator is used to compare a value to all values in another value set ANY: The ANY operator is used to compare a value to any applicable value in the list according to the condition. LIKE: The LIKE operator is used to compare a value to similar values using wildcard operators.It allows to use percent sign(%) and underscore (_) to match a given string pattern. IN: The IN operator is used to compare a value to a list of literal values that have been specified. EXIST: The EXISTS operator is used to search for the presence of a row in a specified table that meets certain criteria.

### SET OPERATORS

The Set operator combines the result of 2 queries into a

The Set operator combines the result of 2 queries into a single result. The following are the operators:

- Union: Returns all distinct rows selected by both the queries.
- Union all: Returns all rows selected by either query including the duplicates.
- Intersect: Returns rows selected that are common to both queries.
- Minus: Returns all distinct rows selected by the first query and are not by the second.

### c) Access Control DCL Language commands

Access Control (DCL): Use GRANT, REVOKE, and ROLE commands to manage user access. - Managing Users: - Create User, Delete User - Managing Passwords - Managing roles: - Grant, Revoke

## Objective

To understand the concept of administrative commands.

## Theory

### DATABASE

DATABASE is collection of coherent data. To create database we have

#### Syntax

```sql
CREATE

DATABASE <database_name>
```

#### Example

```sql
CREATE

DATABASE visionx_db;
```

### TABLESPACE

The oracle database consists of one or more logical storage units called tablespaces. Each tablespace in an Oracle database consists of one or more files called datafiles, which are physical structures that confirm to the operating system in which Oracle is running.

#### Syntax

```sql
CREATE<tablespace name> DATAFILE'C:\oraclexe\app\oracle\product\10.2.0\ server \<file name.dbf ’SIZE 50M;
```

#### Example

```sql
Create tablespace vx_runtime DATAFILE 'C:\oraclexe\app\oracle\product\10.2.0\server\visionx.dbf' SIZE 50M;
```

### CREATE USER

The DBA creates user by executing CREATE USER statement. The user is someone who connects to the database if enough privilege is granted.

#### Syntax

```sql
SQL> CREATE USER < username>

(name of user to be created) IDENTIFIED BY <password> -- (specifies that the user must login with this password)

SQL> user created

Eg: create user visionx_operator identified by vxop123; (The user does not have privilege at this time, it has to be granted.These privileges determine what user can do at database level.)
```

### PRIVILEGES

A privilege is a right to execute an SQL statement or to access another user's object. In Oracle, there are two types of privileges - System Privileges - Object Privileges - System Privileges: are those through which the user can manage the performance of database actions. It is normally granted by DBA to users. Eg: Create Session,Create Table,Create user etc.. - Object Privileges: allow access to objects or privileges on object, i.e. tables, table columns. tables,views etc..It includes alter,delete,insert,select update etc. (After creating the user, DBA grant specific system privileges to user)

### GRANT

The DBA uses the GRANT statement to allocate system privileges to other user.

#### Syntax

```sql
SQL> GRANT

privilege [privilege…. … ] TO

USER

;

SQL> Grant succeeded

Eg: Grant create session, create table, create view to visionx_operator; Object privileges vary from object to object.An owner has all privilege or specific privileges on object.

SQL> GRANT object_priv [(column)]

ON object. TO

user;
SQL>GRANT select, insert ON sessions

TO visionx_operator; SQL>GRANT select,update (device_name,current_status) ON devices TO visionx_operator;
```

### CHANGE PASSWORD

The DBA creates an account and initializes a password for every user.You can change password by using ALTER USER statement.

#### Syntax

```sql
Alter USER <some user name> IDENTIFIED BY<New password>

Eg: ALTER USER visionx_operator IDENTIFIED BY vxop_secure
```

### REVOKE

REVOKE statement is used to remove privileges granted to other users.The privileges you specify are

revoked from the users.

#### Syntax

```sql
REVOKE [privilege..

…] ON object FROM user
```

#### Example

```sql
REVOKE create session,create table from visionx_operator;
REVOKE select,insert ON sessions

FROM visionx_operator
```

### ROLE

A role is a named group of related privileges that can be granted to user.In other words, role is a predefined collection of previleges that are grouped together,thus privileges are easier to assign user.

#### Example

```sql
SQL> Create role visionx_runtime;
SQL> Grant create table,

create view TO visionx_runtime;

SQL> Grant select, insert

ON sessions TO visionx_runtime;
```

Eg: Grant visionx_runtime to visionx_operator, visionx_analyst; C)Transaction Control (TCL): Apply START TRANSACTION,

COMMIT, ROLLBACK, and SAVEPOINT commands to manage

transactions.

## Objective

To understand the concept of administrative commands. A transaction is a logical unit of work. All changes made to the database can be referred to as a transaction. Transaction changes can be made permanent to the database only if they are committed a transaction begins with an executable SQL statement & ends explicitly with either rollback or commit statement.

### 1. COMMIT

This command is used to end a transaction only with

the help of the commit command transaction changes can be made permanent to the database.

#### Syntax

```sql
SQL> COMMIT;
```

#### Example

```sql
SQL> COMMIT;
```

### 2. SAVE POINT

Save points are like marks to divide a very lengthy

transaction to smaller once. They are used to identify a point in a transaction to which we can latter role back. Thus, save point is used in conjunction with role back.

#### Syntax

```sql
SQL> SAVE POINT ID;
```

#### Example

```sql
SQL> SAVE POINT VX_JOBS_QUEUED;
```

### 3. ROLLBACK

A role back command is used to undo the current

transactions. We can role back the entire transaction so that all changes made by SQL statements are undo (or) role back a transaction to a save point so that the SQL statements after the save point are role back.

#### Syntax

```sql
ROLLBACK (current

transaction can be role back)

ROLLBACK to save point
ID;
```

#### Example

```sql
SQL> ROLLBACK;
SQL> ROLLBACK TO SAVE POINT VX_JOBS_QUEUED;
```

## Conclusion

Thus, we have studied and implemented SQL Queries for Data Manipulation, Access Control, Transactions.

## FAQ

1. What are different types of DML commands?
2. What is difference between DML & DDL?
3. Explain the access control on database.
4. What are different types of transaction commands?
