# Assignment No. - 5

## Title

JOIN Operations and Views.

## Problem Statement

Perform various types of JOIN operations to extract meaningful relationships between tables. Create and manage different database views.

## Objective

(a) To learn different types of join and Implementation of different types of Joins - Inner Join - Outer Join - Natural Join..etc. (b) To understand the concept of views & implementation of views.

## Theory

To learn different types of join and Implementation of different types of Joins The SQL Joins clause is used to combine records from two or more tables in a database. A JOIN is a means for combining fields from two tables by using values common to each.The join is actually performed by the ‘where’ clause which combines specified rows of tables.

#### Syntax

```sql
SELECT column 1, column 2, column 3...

FROM table_name1, table_name2 WHERE table_name1.column name = table_name2.columnname;
```

### Types of Joins

### 1. Simple Join

### 2. Self Join

### 3. Outer Join

### Simple Join

It is the most common type of join. It retrieves the rows from 2 tables having a common column and is further classified into

### Equi-join

A join, which is based on equalities, is called equi-join.

#### Example

```sql
Select * from sessions, devices where sessions.device_id=devices.device_id;
```

In the above statement, item-id = cust-id performs the join statement. It retrieves rows from both the tables provided they both have the same id as specified by the where clause. Since the where clause uses the comparison operator (=) to perform a join, it is said to be

It is said to be equijoin. It combines the matched rows of tables. It can be used as follows:

- To insert records in the target table.
- To create tables and insert records in this table.
- To update records in the target table.
- To create views.

### Non Equi-join

It specifies the relationship between columns belonging to different tables by making use of relational operators other than’=’.

#### Example

```sql
Select * from device_health_log, sessions where device_health_log.captured_at<sessions.started_at;
```

### Table Aliases

Table aliases are used to make multiple table queries shorted and more readable. We give an alias name to the table in the ‘from’ clause and use it instead of the name throughout the query.

### Self join

Joining of a table to itself is known as self-join. It joins one row in a table to another. It can compare each row of the table to itself and also with other rows of the same table.

#### Example

```sql
select * from session_events x ,session_events y where x.session_id = y.session_id
and x.event_id < y.event_id;
```

### Outer Join

It extends the result of a simple join. An outer join returns all the rows returned by simple join as well as those rows from one table that do not match any row from the table. The symbol(+) represents outer join. – Left outer join – Right outer join – Full outer join.

#### Example

```sql
SELECT s.session_id,s.session_state,a.result_status
FROM sessions s LEFT OUTER JOIN analysis_results a
ON s.session_id = a.session_id;
```

To understand the concept of views & implementation of views

### VIEW

In SQL, a view is a virtual table based on the result-set of an SQL statement. A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database. You can add SQL functions, WHERE, and JOIN statements to a view and present the data as if the data were coming from one single table. A view is a virtual table, which consists of a set of columns from one or more tables. It is similar to a table but it does not store in the database. View is a query stored as an object.

#### Syntax

```sql
CREATE VIEW <view_name> AS SELECT <set of fields> FROM

relation_name WHERE (Condition)
```

#### Example

```sql
SQL> CREATE VIEW visionx_session_view AS SELECT session_id,device_id,session_state FROM SESSIONS WHERE session_state = 'COMPLETE';
SQL>
View created.
```

#### Example

```sql
CREATE VIEW visionx_failed_results AS SELECT session_id,
result_kind
FROM analysis_results
WHERE result_status='FAILED';
```

### UPDATING A VIEW

A view can updated by using the following syntax

#### Syntax

```sql
CREATE OR REPLACE VIEW view_name AS SELECT column_name(s)

FROM table_name WHERE condition
```

### DROPPING A VIEW

A view can deleted with the DROP VIEW command.

#### Syntax

```sql
DROP VIEW <view_name>;
```

## Conclusion

Thus, we have studied various types of JOIN operations to extract meaningful relationships

between tables. Implemented the different join commands & database views.

## FAQ

1. What is join operation?
2. What are different types of join?
3. Give examples of join operation.
4. What is view?
5. Give a example of view.
