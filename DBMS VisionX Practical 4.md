# Assignment No. - 4

## Title

Aggregate Functions and Grouping.

## Problem Statement

SQL Queries for aggregate functions along with GROUP BY and HAVING clauses to retrieve summarized data from the database.

## Objective

To learn the concept of following group functions & implement clauses to retrieve summarized data from the database.

- Group by & Having Clause
- Order by Clause
- Indexing

## Theory

### GROUP BY

This query is used to group to all the records in a relation together for each and every value of a specific key(s) and then display them for a selected set of fields the relation.

#### Syntax

```sql
SELECT <set of fields> FROM <relation_name>

GROUP BY <field_name>;
```

#### Example

```sql
SQL> SELECT DEVICE_ID, COUNT(SESSION_ID) FROM SESSIONS GROUP BY DEVICE_ID;
```

### GROUP BY-HAVING

The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions. The HAVING clause must follow the GROUP BY clause in a query and must also precede the ORDER BY clause if used.

#### Syntax

```sql
SELECT column_name, aggregate_function(column_name) FROM table_name

WHERE column_name operator value GROUP BY column_name HAVING aggregate_function(column_name) operator value;
```

#### Example

```sql
SELECT SESSIONS.SESSION_STATE, COUNT(ANALYSIS_JOBS.JOB_ID)
AS FAILED_JOBS FROM (SESSIONS
INNER JOIN ANALYSIS_JOBS
ON SESSIONS.SESSION_ID=ANALYSIS_JOBS.SESSION_ID)
GROUP BY SESSION_STATE HAVING COUNT
(ANALYSIS_JOBS.JOB_ID) > 0;
```

### JOIN using GROUP BY

This query is used to display a set of fields from two relations by matching a common field in them and also group the corresponding records for each and every value of a specified key(s) while displaying.

#### Syntax

```sql
SELECT <set of fields (from both relations)> FROM

relation_1,relation_2 WHERE relation_1.field_x=relation_2.field_y GROUP BY

field_z;
```

#### Example

```sql
SQL> SELECT d.device_name,COUNT(s.session_id)
FROM devices d,sessions s WHERE
d.device_id = s.device_id GROUP BY
d.device_name;
```

### ORDER BY

This query is used to display a selected set of fields from a relation in an ordered manner base on some field.

#### Syntax

```sql
SELECT <set of fields>

FROM <relation_name>

ORDER BY

<field_name>;
```

#### Example

```sql
SQL> SELECT session_id, session_state, frame_count FROM sessions ORDER BY frame_count DESC;
```

### JOIN using ORDER BY

This query is used to display a set of fields from two relations by matching a common field in them in an ordered manner based on some fields.

#### Syntax

```sql
SELECT <set of fields (from both relations)> FROM

relation_1, relation_2 WHERE relation_1.field_x = relation_2.field_y ORDER BY field_z;
```

#### Example

```sql
SQL> SELECT d.device_name,s.session_id,s.session_state
FROM devices d,sessions s WHERE
d.device_id = s.device_id ORDER BY d.device_name;
```

### INDEXING

An index is an ordered set of pointers to the data in a table. It is based on the data values in one or more columns of the table. SQL Base stores indexes separately from tables.

### An index provides two benefits

- It improves performance because it makes data access faster. - It ensures uniqueness. A table with a unique index cannot have two rows with the same values in the column or columns that form the index key.

#### Syntax

```sql
CREATE INDEX <index_name> on <table_name> (attrib1,attrib

2….attrib n);
```

#### Example

```sql
CREATE INDEX idx_sessions_device_state on sessions(device_id,session_state);
```

## Conclusion

Thus, we have studied the SQL Queries for aggregate functions along with GROUP BY and HAVING clauses and implemented to retrieve summarized data from the database.

## FAQ

1. What is aggregation?
2. What is mean by grouping?
3. What is syntax of having command?
4. How to use group by command?
