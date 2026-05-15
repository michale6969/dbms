# Super Simple DBMS Practical Queries (1 to 10)

This version is intentionally basic.

- Practicals 1 to 8: Oracle SQL / PL-SQL
- Practicals 9 and 10: MongoDB


## Practical 1: Basic student database setup

### Commands + what they do

```sql
-- Creates student table (main student info)
CREATE TABLE student (
  student_id NUMBER PRIMARY KEY,
  student_name VARCHAR2(40) NOT NULL,
  department VARCHAR2(30)
);

-- Creates subject table (subject list)
CREATE TABLE subject (
  subject_id NUMBER PRIMARY KEY,
  subject_name VARCHAR2(40) NOT NULL
);

-- Creates marks table (links student and subject with marks)
CREATE TABLE marks (
  mark_id NUMBER PRIMARY KEY,
  student_id NUMBER,
  subject_id NUMBER,
  total_marks NUMBER(3),
  grade VARCHAR2(2),
  FOREIGN KEY (student_id) REFERENCES student(student_id),
  FOREIGN KEY (subject_id) REFERENCES subject(subject_id)
);

-- Inserts sample students
INSERT INTO student VALUES (1, 'Aarav', 'Computer');
INSERT INTO student VALUES (2, 'Riya', 'Computer');
INSERT INTO student VALUES (3, 'Neha', 'Electronics');

-- Inserts sample subjects
INSERT INTO subject VALUES (101, 'DBMS');
INSERT INTO subject VALUES (102, 'DS');

-- Inserts sample marks
INSERT INTO marks VALUES (1, 1, 101, 84, 'A+');
INSERT INTO marks VALUES (2, 2, 101, 92, 'O');
INSERT INTO marks VALUES (3, 3, 102, 69, 'B+');

-- Saves all inserts
COMMIT;
```

## Practical 2: DDL commands and constraints

### Commands + what they do

```sql
-- CREATE: makes a new table with constraints
CREATE TABLE ddl_demo (
  id NUMBER PRIMARY KEY,
  name VARCHAR2(30) NOT NULL,
  email VARCHAR2(50) UNIQUE,
  age NUMBER CHECK (age >= 18)
);

-- ALTER: adds new column
ALTER TABLE ddl_demo ADD city VARCHAR2(20);

-- ALTER RENAME COLUMN: renames one column
ALTER TABLE ddl_demo RENAME COLUMN city TO hometown;

-- RENAME TABLE: renames the table
RENAME ddl_demo TO ddl_demo_new;

-- TRUNCATE: removes all rows but keeps table
TRUNCATE TABLE ddl_demo_new;

-- DROP: deletes table completely
DROP TABLE ddl_demo_new;
```

## Practical 3: DML, operators, DCL, TCL

### DML commands

```sql
-- INSERT: adds one row
INSERT INTO student VALUES (4, 'Karan', 'Computer');

-- UPDATE: changes marks for one student
UPDATE marks
SET total_marks = total_marks + 1
WHERE student_id = 1;

-- DELETE: removes one row
DELETE FROM student
WHERE student_id = 4;

-- Saves DML changes
COMMIT;
```

### Operator and function examples

```sql
-- Arithmetic + logical: adds bonus marks and filters
SELECT student_id, total_marks, total_marks + 5 AS bonus_marks
FROM marks
WHERE total_marks > 70;

-- Pattern matching: names starting with A
SELECT * FROM student
WHERE student_name LIKE 'A%';

-- String function: uppercase name
SELECT student_id, UPPER(student_name) AS upper_name
FROM student;

-- Set operator: combines student IDs from two queries
SELECT student_id FROM student
UNION
SELECT student_id FROM marks;
```

### DCL commands

```sql
-- Creates a role
CREATE ROLE simple_read_role;

-- Gives SELECT permission on student table to role
GRANT SELECT ON student TO simple_read_role;

-- Gives role to user (replace lab_user if needed)
GRANT simple_read_role TO lab_user;

-- Removes role from user
REVOKE simple_read_role FROM lab_user;
```

### TCL commands

```sql
-- Starts change 1
UPDATE student SET department = 'CSE' WHERE student_id = 1;

-- Saves a rollback point
SAVEPOINT sp1;

-- Starts change 2
UPDATE student SET department = 'IT' WHERE student_id = 1;

-- Undoes only change 2
ROLLBACK TO sp1;

-- Final commit
COMMIT;
```

## Practical 4: Aggregate, GROUP BY, HAVING, ORDER BY, index

### Commands + what they do

```sql
-- GROUP BY: counts students in each department
SELECT department, COUNT(*) AS total_students
FROM student
GROUP BY department;

-- HAVING: keeps only subject groups with avg marks > 70
SELECT subject_id, AVG(total_marks) AS avg_marks
FROM marks
GROUP BY subject_id
HAVING AVG(total_marks) > 70;

-- ORDER BY: sorts marks high to low
SELECT student_id, total_marks
FROM marks
ORDER BY total_marks DESC;

-- INDEX: makes search by student_id faster
CREATE INDEX idx_marks_student ON marks(student_id);
```

## Practical 5: JOIN operations and view

### Commands + what they do

```sql
-- INNER JOIN: only matching rows from all tables
SELECT s.student_name, sub.subject_name, m.total_marks
FROM student s
JOIN marks m ON s.student_id = m.student_id
JOIN subject sub ON sub.subject_id = m.subject_id;

-- LEFT JOIN: all students, even if marks missing
SELECT s.student_name, m.total_marks
FROM student s
LEFT JOIN marks m ON s.student_id = m.student_id;

-- RIGHT JOIN: all marks, even if student row missing
SELECT s.student_name, m.total_marks
FROM student s
RIGHT JOIN marks m ON s.student_id = m.student_id;

-- FULL OUTER JOIN: keeps all rows from both sides
SELECT s.student_name, m.total_marks
FROM student s
FULL OUTER JOIN marks m ON s.student_id = m.student_id;

-- SELF JOIN: pairs students from same department
SELECT a.student_name AS student1, b.student_name AS student2, a.department
FROM student a
JOIN student b ON a.department = b.department AND a.student_id < b.student_id;
```

```sql
-- VIEW: creates virtual table for quick score view
CREATE OR REPLACE VIEW v_score AS
SELECT s.student_name, sub.subject_name, m.total_marks, m.grade
FROM student s
JOIN marks m ON s.student_id = m.student_id
JOIN subject sub ON sub.subject_id = m.subject_id;

-- Shows data from the view
SELECT * FROM v_score;

-- Deletes the view
DROP VIEW v_score;
```

## Practical 6: Subqueries

### Commands + what they do

```sql
-- Subquery with AVG: gets students above average marks
SELECT DISTINCT s.student_name
FROM student s
JOIN marks m ON s.student_id = m.student_id
WHERE m.total_marks > (SELECT AVG(total_marks) FROM marks);

-- Subquery with IN: gets students with high grades
SELECT student_name
FROM student
WHERE student_id IN (
  SELECT student_id
  FROM marks
  WHERE grade IN ('A+', 'O')
);

-- Correlated subquery: compares marks inside same subject
SELECT m1.student_id, m1.subject_id, m1.total_marks
FROM marks m1
WHERE m1.total_marks > (
  SELECT AVG(m2.total_marks)
  FROM marks m2
  WHERE m2.subject_id = m1.subject_id
);
```

## Practical 7: Procedure, function, cursor

### Commands + what they do

```sql
-- Allows DBMS_OUTPUT messages in SQL*Plus/SQL Developer
SET SERVEROUTPUT ON;

-- Function: returns best marks of one student
CREATE OR REPLACE FUNCTION fn_best_marks(p_student_id NUMBER)
RETURN NUMBER
IS
  v_marks NUMBER;
BEGIN
  SELECT MAX(total_marks) INTO v_marks
  FROM marks
  WHERE student_id = p_student_id;

  RETURN NVL(v_marks, 0);
END;
/
```

```sql
-- Procedure with cursor: prints all student names with marks
CREATE OR REPLACE PROCEDURE pr_show_marks
IS
  CURSOR c1 IS
    SELECT s.student_name, m.total_marks
    FROM student s
    JOIN marks m ON s.student_id = m.student_id;
BEGIN
  FOR r IN c1 LOOP
    DBMS_OUTPUT.PUT_LINE(r.student_name || ' : ' || r.total_marks);
  END LOOP;
END;
/

-- Runs procedure
EXEC pr_show_marks;

-- Calls function in SELECT
SELECT student_id, fn_best_marks(student_id) AS best_marks
FROM student;
```

## Practical 8: Triggers

### Setup commands

```sql
-- Creates sequence for audit IDs
CREATE SEQUENCE audit_seq START WITH 1 INCREMENT BY 1;

-- Creates audit table to store name changes
CREATE TABLE student_audit (
  audit_id NUMBER PRIMARY KEY,
  student_id NUMBER,
  old_name VARCHAR2(40),
  new_name VARCHAR2(40),
  changed_on DATE
);
```

### Trigger commands

```sql
-- BEFORE trigger: auto-sets grade from total_marks
CREATE OR REPLACE TRIGGER trg_set_grade
BEFORE INSERT OR UPDATE OF total_marks ON marks
FOR EACH ROW
BEGIN
  IF :NEW.total_marks >= 90 THEN :NEW.grade := 'O';
  ELSIF :NEW.total_marks >= 80 THEN :NEW.grade := 'A+';
  ELSIF :NEW.total_marks >= 70 THEN :NEW.grade := 'A';
  ELSE :NEW.grade := 'B+';
  END IF;
END;
/
```

```sql
-- AFTER trigger: saves old/new student name in audit table
CREATE OR REPLACE TRIGGER trg_audit_name
AFTER UPDATE OF student_name ON student
FOR EACH ROW
BEGIN
  INSERT INTO student_audit
  VALUES (audit_seq.NEXTVAL, :OLD.student_id, :OLD.student_name, :NEW.student_name, SYSDATE);
END;
/

-- Test trigger
UPDATE student SET student_name = 'Aarav K' WHERE student_id = 1;
SELECT * FROM student_audit;
COMMIT;
```

## Practical 9: MongoDB CRUD (+ save + logical operators)

### Commands + what they do

```javascript
use student_practicals_db

// Removes old collection data
db.students.drop()

// CREATE: inserts documents
db.students.insertOne({ _id: 1, name: "Aarav", dept: "Computer", cgpa: 8.4 })
db.students.insertOne({ _id: 2, name: "Riya", dept: "Computer", cgpa: 9.1 })
db.students.insertOne({ _id: 3, name: "Neha", dept: "Electronics", cgpa: 7.8 })

// save(): updates if _id exists, inserts if not
db.students.save({ _id: 3, name: "Neha J", dept: "Electronics", cgpa: 8.0 })

// READ: shows all
db.students.find()

// READ with logical operator OR
db.students.find({ $or: [ { cgpa: { $gt: 9 } }, { name: "Aarav" } ] })

// UPDATE
db.students.updateOne({ _id: 1 }, { $set: { dept: "CSE" } })

// DELETE
db.students.deleteOne({ _id: 2 })
```

## Practical 10: MongoDB aggregation and indexing

### Commands + what they do

```javascript
use student_practicals_db

// Clears old marks collection
db.marks.drop()

// Adds sample marks documents
db.marks.insertMany([
  { _id: 1, studentId: 1, subject: "DBMS", marks: 84 },
  { _id: 2, studentId: 1, subject: "DS", marks: 78 },
  { _id: 3, studentId: 3, subject: "DBMS", marks: 69 }
])

// Aggregation: average marks per subject
db.marks.aggregate([
  { $group: { _id: "$subject", avgMarks: { $avg: "$marks" } } }
])

// Aggregation: highest marks per student
db.marks.aggregate([
  { $group: { _id: "$studentId", maxMarks: { $max: "$marks" } } }
])

// Creates simple indexes
db.students.createIndex({ name: 1 })
db.marks.createIndex({ studentId: 1, subject: 1 })

// Shows indexes
db.students.getIndexes()
db.marks.getIndexes()
```
