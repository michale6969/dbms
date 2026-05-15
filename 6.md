# Assignment No. - 6

## Title

Study & Implementation of sub-queries.

## Problem Statement

Write and execute sub-queries to retrieve data from one table based on results from another.

## Objective

To perform nested queries using DML command. To implement and execute sub-queries to retrieve data from database.

## Theory

SUBQUERIES: The query within another is known as a sub query. A statement containing sub query is called parent statement. The rows returned by sub query are used by the parent statement or in other words A subquery is a SELECT statement that is embedded in a clause of another SELECT statement

You can place the subquery in a number of SQL clauses:

- WHERE clause
- HAVING clause
- FROM clause
- OPERATORS(IN.ANY,ALL,<,>,>=,<= etc..)

### Types

1.Sub queries that return several values

Sub queries can also return more than one value. Such results should be made use along with the operators in and any.

2.Multiple queries

Here more than one sub query is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.

3.Correlated sub query

A sub query is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

#### Example

```sql
SELECT SESSION_ID, SESSION_STATE
FROM SESSIONS
WHERE DEVICE_ID IN (
    SELECT DEVICE_ID
    FROM DEVICES
    WHERE CURRENT_STATUS = 'RECORDING'
);

SELECT SESSION_ID, FRAME_COUNT
FROM SESSIONS
WHERE SESSION_ID IN (
    SELECT SESSION_ID
    FROM ANALYSIS_JOBS
    WHERE JOB_STATUS = 'FAILED'
)
AND DEVICE_ID IN (
    SELECT DEVICE_ID
    FROM DEVICE_HEALTH_LOG
    WHERE REACHABLE_FLAG = 'N'
);

SELECT S.SESSION_ID, S.DEVICE_ID, S.FRAME_COUNT
FROM SESSIONS S
WHERE S.FRAME_COUNT > (
    SELECT AVG(S2.FRAME_COUNT)
    FROM SESSIONS S2
    WHERE S2.DEVICE_ID = S.DEVICE_ID
);
```

## Conclusion

Thus, we have studied & Implemented the sub-queries for a database.

## FAQ

1. What is mean by sub-query?
2. Which different commands are used in sub-query?
3. Give examples of sub-query operation.
4. How to use multiple queries within a query?
