# Assignment No. - 8

## Title

Database Triggers.

## Problem Statement

Implement and test triggers to maintain data integrity in database.

## Objective

- To learn concept of of trigger.
- To implement trigger in PL/SQL.

### DATABASE TRIGGERS

A database trigger is a PL/SQL program unit, which gets fired automatically whenever the data event such as DML or DDL system event. Triggers are associated with a specific table and are fired automatically whenever the table gets manipulated in a predefined way. The act of executing a trigger is called as firing a trigger. Triggers are similar to procedures in that they are named PL/SQL blocks with declarative, executable and exception handling sections. But the difference is a procedure is executed explicitly from another block via a procedure call but a trigger is executed implicitly whenever the triggering event happens. A procedure can pass arguments but trigger doesn‟t accept

A database trigger has following components:

1. A triggering Event
2. A triggering Constraint
3. A triggering Action

Trigger categories are categorized in various ways.

### Trigger type

Triggering time Triggering event Trigger types There are two types of triggers.

Statement Trigger:-A statement trigger is a trigger in which the trigger action is executed once for the manipulation operation that fires the trigger.

Row Trigger:-A row trigger is a trigger in which the trigger action is performed repeatedly for each row of the table that is affected by the manipulation operation that fires the trigger.

### Triggering time

Triggers can specify the time of trigger action.

Before the triggering event The trigger action is performed before the operation that fires the trigger is executed. This trigger is used when execution of operation depends on trigger action.

After the triggering event The trigger action is performed after the operation that fires the trigger is executed. This trigger is used when triggering action depends on the execution of operation.

Triggering Events Triggering events are the DML operations. These operations are insert, update and delete. When these operations are performed on a table, the trigger which is associated with the operation is fired.

Triggering events divide triggers into three types:

- INSERT TRIGGER
- DELETE TRIGGER
- UPDATE TRIGGER

### General syntax for creation of Trigger

#### Syntax

```sql
Create [or replace] TRIGGER <trigger_name> <BEFORE | AFTER>
DELETE
| [OR] INSERT
| [OR] UPDATE [OF <column1>[,<column2>…..]
ON <table_name>
[for each row]
[when <condition>]
BEGIN
    ………
END;
```

Where

Trigger_name:-trigger name is the name of the trigger. Table_name:-is thye table name for which ger is defined.Trigger-condition:-The trigger condition in the when clause,if present is evaluates The body of the trigger is executed only when this condition evaluates to true.

### Dropping trigger

Suppose you want to drop trigger then the syntax is.

#### Syntax

```sql
Drop trigger trigger_name;
```

### Enabling and Disabling Triggers

The Trigger can be disabled without dropping them. When the trigger is disabled, it is still exists in data dictionary but never fired. To disable trigger, use alter command.

#### Syntax

```sql
Alter TRIGGER trigger_name DISABLE/ENABLE;
```

For all triggers on a particular table

#### Syntax

```sql
Alter TRIGGER trigger_name (DISABLE/ENABLE) all triggers;
```

### VisionX Trigger Example

```sql
CREATE OR REPLACE TRIGGER trg_analysis_jobs_audit
BEFORE INSERT OR UPDATE ON analysis_jobs
FOR EACH ROW
BEGIN
    IF INSERTING THEN
        :NEW.created_at := NVL(:NEW.created_at, SYSDATE);
    END IF;
    :NEW.updated_at := SYSDATE;
END;
/

CREATE OR REPLACE TRIGGER trg_session_time_check
BEFORE INSERT OR UPDATE ON sessions
FOR EACH ROW
BEGIN
    IF :NEW.ended_at IS NOT NULL AND :NEW.ended_at < :NEW.started_at THEN
        RAISE_APPLICATION_ERROR(-20001, 'ENDED_AT cannot be earlier than STARTED_AT');
    END IF;
END;
/

ALTER TRIGGER trg_analysis_jobs_audit DISABLE;
ALTER TRIGGER trg_analysis_jobs_audit ENABLE;
DROP TRIGGER trg_session_time_check;
```

## Conclusion

Thus we have studied the concept of trigger in PL/SQL and implemented.

## FAQ

1. Write a database Trigger.
2. Explain Database Trigger Components.
3. Explain Trigger Types with e.g.
4. Explain difference between Row-Level & Statement-Level Trigger.
5. Write a Syntax for Enable & Disable Trigger.
6. Write a Syntax for Displaying Trigger Errors.
