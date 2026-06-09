## What is a Database?
Where we store the data in a organize way annd can be access easily.

## What is RDBMS?
where we can connect tables to each other and uses SQL for managing and querying data.

## SQL
Structured Query Language
Which is used to talk to our databases.

### Some Important Queries in SQL SHELL
``` sql
\l         - list all databases
\q         - quit
\c db_name - connect to database
\dt        - list all tables
\d tb_name - desc a table
\d+ tb_name- list all column
\! cls.    - list all column
```
#### IMPORTANT QUERY
``` sql
//SHOW ALL EXISTING DB
SELECT datname FROM pg_database;

// CREATE DB
CREATE DATABASE <db_name>;

// DELETE DB
DROP DATABASE <db_name>;

// CREATE TABLE
CREATE TABLE person ( 
  id INT,
  name VARCHAR(100),
  city VARCHAR(100)
); 

//Adding data into a Table
INSERT INTO person(id, name, city) 
  VALUES (101, ‘Raju’, ‘Delhi’);

// READ TANLE
SELECT * FROM <table_name> 

// Modify/Update data from a Table
UPDATE person
    SET city=’London’ 
    WHERE id=2;

//DELETE data from a Table
DELETE FROM students
WHERE name='Raju';

// ### USING WHERE CLAUSE
// READ 
SELECT * FROM tablename
WHERE ID = 1;

//UPDATE
UPDATE tbname SET contact = 1234 WHERE ID = 01;

// DELETE
DELETE FROM tbname WHERE ID = 104;

// PRIMARY KEY / DEFAULT /NOT NULL/ AUTO INCREAMENT
CREATE TABLE person ( 
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  city VARCHAR(100) NOT NULL,
SALARY VARCHAR(100) NOT NULL DEFAULT = 25000
); 
```
  
## CLAUSE
Giving some conditions With SQL Queries called clause.

``` sql

// WHERE CLAUSE
SELECT * FROM tablename
WHERE salary < 20000;

/* DISTICT
IT IS USED TO SHOW UNIQUE DATA FROM TABLE INSTEAD OF DUPPLICATW
*/

SELECT DISTINCT dept FROM tbname;

// IN & NOT IN
IN - IS USE TO SEE THE ONLY MENTION DATA WITH IN.
NOT IN - IS USED TO IGNORE THE DATA MENTION WITH NOT IN .

SELECT * FROM employees 
WHERE dept IN ('IT', 'HR', 'Finance');

// NOT IN
SELECT * FROM employees 
WHERE dept NOT IN ('IT', 'HR', 'Finance');

// BETWEEN - is use to see the vaue mid of two ranges
SELECT * FROM employees 
WHERE 
salary BETWEEN 40000 AND 65000;

// ORDER BY - ITS USE TO ARRANGE OR SORT THE DATA BY GIVING SOME CONDITION .
SELECT * FROM employees ORDER BY fname;

// ### OUTPUT
ASHISH
BHARAT
CHANDU

// LIMIT - ITS USED TO SHOW THE LIMITED DATA BY ASIGNING SOME LIMIT .
SELECT * FROM employees LIMIT 3;

/* LIKE - ITS USE TO SEARCH DATA WITH ALPHABETS e.g
Name start with A - 'A%'
Name end with i - '%i'
Name mid word s - '%s%'
or
Starts with 'A': LIKE 'A%'
Ends with 'A': LIKE '%A'
Contains 'A': LIKE '%A%'
Second character is 'A': LIKE '_A%'
Case-insensitive contains 'john': ILIKE '%john%'*/

Select * FROM employees 
 WHERE dept LIKE "%Acc%";

/* GROUP BY
used to create the group of data based on how many belong from same data*/
SELECT dept FROM employees GROUP BY dept;

SELECT dept, COUNT(fname) FROM employees GROUP BY dept;

```
### AGREGATE FUNCTIONS
function which perform some operation on table called agregate function.

``` sql
// COUNT
SELECT COUNT(user_id) FROM employees;

// MAX & MIN
SELECT MAX(age) FROM employees;

SELECT MIN(age) FROM employees;

// TO FIND MAX OR MIN SALARY
SELECT emp_id, fname, salary FROM employees
 WHERE 
salary = (SELECT MAX(salary) FROM employees);

// SUM & AVG
SELECT SUM(salary) FROM employees;

SELECT AVG(salary) FROM employees;

```
### STRING FUNCTIONS 
``` sql
/* CONCAT - IT IS USED TO COMBINE TWO TABLE
AND SHOW A NEW TABLE WITH COMBINATION OF TWO TABLE*/
CONCAT(first_col, sec_col) 
CONCAT(first_word, sec_word, ...)

/* CONCAT_WS (WITH SEPERATOR)
USE TO ADD SPACE _: ETC BETWEEN NAMES*/
CONCAT_WS('-', fname, lname)

/* SUBSTRING
IS USED TO GET THE SUBSTRING OF ANY LETTER */
SELECT SUBSTRING('Hey Buddy', 1, 4); 

1
4
Result: Hey

// REPLACE - IT IS USED TO REPLACE THE LETTER FROM A STRING
REPLACE(str, from_str, to_str)

REPLACE('Hey Buddy', 'Hey', 'Hello')

Result: Hello Buddy

// REVERSE - it is used to reverse the string name etc.
SELECT REVERSE('Hello');

Result: olleH


// LENGTH - used to calculate the length of string.
Select LENGTH('Hello World');

Result: 11.

// UPPER & LOWER
SELECT UPPER('Hello World');

SELECT LOWER('Hello World');

// LEFT - IT IS USED TO SEE THE LEFT SIDE DATA OF STRING
SELECT LEFT('Abcdefghij', 3);

Result: Abc

// RIGHT - IT IS USED TO SEE THE RIGHT SIDE DATA OF STRING
SELECT RIGHT('Abcdefghij', 4);

Result: ghij

// TRIM - used to remove the side and extra space from a string.
SELECT TRIM('  Alright!  '); 

// POSITION -use to see the position of text or letter.
SELECT POSITION('OM' in ‘Thomas’);

Result: 3
```
### ALTER TABLE
``` sql
// to rename a column name
ALTER TABLE tb_name
RENAME COLUMN name TO full_name;

// to rename a  table name
RENAME TABLE contract TO mycontract;

// to add or remove a column
ALTER TABLE tb_name
ADD COLUMN city VARCHAR(100);

ALTER TABLE tb_name
DROP COLUMN city:


// to modify a column- Changing data types and the values.
ALTER TABLE tb_name
ALTER COLUMN fname
SET DATA TYPE VARCHAR(150);

//
ALTER TABLE tb_name
ALTER COLUMN fname
SET NOT NULL;
```

### CHECK CONSTRAINT - its used to add restriction based on some condition 
``` sql
// We want to make sure phone no. is atleast 10 digits...
CREATE TABLE tb_name(
name VARCHAR(50),
mob VARCHAR(15) CHECK (LENGTH (mob) >=10));

// TO DELETE IT
ALTER TABLE tb_name
DROP CONNSTRAINT mob;

// Here contraint is used to show the error or msg if user enter the wrong value 
CREATE TABLE tb_name
ADD CONTRAINT mob_num_less_than_10_digits CHECK (LENGTH (mob) >=10));

```
### CASE - use to create a separate comun with some value on condition 
``` sql
SELECT fname, salary,
CASE WHEN salary >= THEN 'High' ELSE 'Low'
ENS AS sal_cat FROM employee/tb_name;


SELECT fname, salary,
CASE WHEN salary >=50000 THEN 'High'
WHEN salary BETWEEN 40000 AND 50000 THEN 'Mid' ELSE 'Low'
ENS AS sal_cat FROM employee/tb_name;
```
## RELATIONSHIPS IN DATABASE

Relationship means connecting one table with another table using keys.

### Types of Relationships

1. One To One (1:1)
2. One To Many (1:N)
3. Many To One (N:1)
4. Many To Many (M:N)

---

## FOREIGN KEY

Foreign Key is used to connect two tables.

It creates a relationship between parent table and child table.

### Syntax

```sql
CREATE TABLE department(
    dept_id SERIAL PRIMARY KEY,
    dept_name VARCHAR(100)
);

CREATE TABLE employee(
    emp_id SERIAL PRIMARY KEY,
    emp_name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY(dept_id)
    REFERENCES department(dept_id)
);
```

## ONE TO ONE RELATIONSHIP (1:1)

One record from Table A can be connected with only one record from Table B.

### Example

Every person has only one passport.

```sql
CREATE TABLE person(
    person_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE passport(
    passport_id INT PRIMARY KEY,
    person_id INT UNIQUE,
    FOREIGN KEY(person_id)
    REFERENCES person(person_id)
);
```
---

## ONE TO MANY RELATIONSHIP (1:N)

One record from parent table can have many records in child table.

### Example

One department can have many employees.

```sql
DEPARTMENT
-----------
IT
HR

EMPLOYEE
-----------
Rahul -> IT
Aman  -> IT
Rohit -> HR
```

```sql
CREATE TABLE department(
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY(dept_id)
    REFERENCES department(dept_id)
);
```

## MANY TO MANY RELATIONSHIP (M:N)

Many records from Table A can connect with many records from Table B.

### Example

Students and Courses

One student can enroll in many courses.

One course can have many students.

To implement this relationship we create a Junction Table (Bridge Table).

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

CREATE TABLE courses(
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);

CREATE TABLE student_course(
    student_id INT,
    course_id INT,

    PRIMARY KEY(student_id, course_id),

    FOREIGN KEY(student_id)
    REFERENCES students(student_id),

    FOREIGN KEY(course_id)
    REFERENCES courses(course_id)
);
```

### Sample Data

```sql
INSERT INTO students VALUES
(1,'Rahul'),
(2,'Aman');

INSERT INTO courses VALUES
(101,'Java'),
(102,'SQL');

INSERT INTO student_course VALUES
(1,101),
(1,102),
(2,101);
```

### Output

```text
Rahul -> Java
Rahul -> SQL
Aman  -> Java
```

---

# JOINS

Join is used to combine data from multiple tables based on a common column.

---

## INNER JOIN

Returns only matching records from both tables.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employee e
INNER JOIN department d
ON e.dept_id = d.dept_id;
```

### Output

```text
Rahul   IT
Aman    HR
```

---

## LEFT JOIN

Returns all records from left table and matching records from right table.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employee e
LEFT JOIN department d
ON e.dept_id = d.dept_id;
```

### Output

```text
Rahul   IT
Aman    HR
Rohit   NULL
```

---

## RIGHT JOIN

Returns all records from right table and matching records from left table.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employee e
RIGHT JOIN department d
ON e.dept_id = d.dept_id;
```

---

## FULL OUTER JOIN

Returns all records from both tables.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employee e
FULL OUTER JOIN department d
ON e.dept_id = d.dept_id;
```

---

## CROSS JOIN

Returns Cartesian Product.

Every row of first table is combined with every row of second table.

```sql
SELECT *
FROM employee
CROSS JOIN department;
```

### Example

```text
EMPLOYEE = 3 Rows
DEPARTMENT = 2 Rows

RESULT = 3 × 2 = 6 Rows
```

---

## SELF JOIN

A table joined with itself.

### Example

Employee and Manager stored in same table.

```sql
CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    manager_id INT
);
```

```sql
SELECT e.emp_name AS Employee,
       m.emp_name AS Manager
FROM employee e
LEFT JOIN employee m
ON e.manager_id = m.emp_id;
```

---

## DIFFERENCE BETWEEN PRIMARY KEY AND FOREIGN KEY

| PRIMARY KEY | FOREIGN KEY |
|------------|------------|
| Uniquely identifies a record | Connects two tables |
| Cannot contain NULL | Can contain NULL |
| One per table | Multiple allowed |
| Prevents duplicate values | Allows duplicate values |



# VIEW

A View is a virtual table created using a SQL query.

It does not store data physically. It shows data from one or more tables.

### Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name;
```

### Example

```sql
CREATE VIEW emp_view AS
SELECT emp_id, emp_name, department
FROM employees;
```

### Use View

```sql
SELECT * FROM emp_view;
```

### Delete View

```sql
DROP VIEW emp_view;
```

---

# HAVING CLAUSE

HAVING is used to filter grouped data.

WHERE filters rows.

HAVING filters groups.

### Syntax

```sql
SELECT column_name,
       COUNT(*)
FROM table_name
GROUP BY column_name
HAVING condition;
```

### Example

```sql
SELECT department,
       COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

### Difference Between WHERE and HAVING

| WHERE | HAVING |
|---------|---------|
| Filters rows | Filters groups |
| Used before GROUP BY | Used after GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |

---

# STORED PROCEDURE

A Stored Procedure is a saved SQL block that can be executed whenever needed.

### Syntax

```sql
CREATE OR REPLACE PROCEDURE procedure_name()
LANGUAGE plpgsql
AS $$
BEGIN

    -- SQL Statements

END;
$$;
```

### Example

```sql
CREATE OR REPLACE PROCEDURE get_message()
LANGUAGE plpgsql
AS $$
BEGIN
    RAISE NOTICE 'Procedure Executed';
END;
$$;
```

### Execute Procedure

```sql
CALL get_message();
```

---

# USER DEFINED FUNCTION (UDF)

A User Defined Function is a custom function created by the user.

It must return a value.

### Syntax

```sql
CREATE FUNCTION function_name()
RETURNS datatype
AS $$
BEGIN

    RETURN value;

END;
$$ LANGUAGE plpgsql;
```

### Example

```sql
CREATE FUNCTION get_bonus(
    salary INT
)
RETURNS INT
AS $$
BEGIN

    RETURN salary * 10 / 100;

END;
$$ LANGUAGE plpgsql;
```

### Execute Function

```sql
SELECT get_bonus(50000);
```

### Output

```text
5000
```

---

# WINDOW FUNCTION

Window Functions perform calculations across a set of rows without grouping them.

Unlike GROUP BY, they do not reduce the number of rows.

### Syntax

```sql
SELECT column_name,
       window_function()
       OVER(...)
FROM table_name;
```

### ROW_NUMBER()

Assigns a unique number to each row.

```sql
SELECT emp_name,
       ROW_NUMBER()
       OVER(ORDER BY salary DESC)
FROM employees;
```

### RANK()

Assigns rank based on a condition.

```sql
SELECT emp_name,
       salary,
       RANK()
       OVER(ORDER BY salary DESC)
FROM employees;
```

### Running Total

```sql
SELECT emp_name,
       salary,
       SUM(salary)
       OVER(ORDER BY emp_id)
FROM employees;
```

---

# CTE (COMMON TABLE EXPRESSION)

A CTE is a temporary result set created using WITH.

It makes complex queries easier to read.

### Syntax

```sql
WITH cte_name AS
(
    query
)
SELECT *
FROM cte_name;
```

### Example

```sql
WITH high_salary AS
(
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary;
```

### Benefits

- Improves readability
- Breaks complex queries into parts
- Can be reused within the query

---

# TRIGGERS

A Trigger is a block of code that executes automatically when an event occurs.

### Events

- INSERT
- UPDATE
- DELETE

### Steps

#### 1. Create Trigger Function

```sql
CREATE OR REPLACE FUNCTION log_message()
RETURNS TRIGGER
AS $$
BEGIN

    RAISE NOTICE 'New Record Inserted';

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### 2. Create Trigger

```sql
CREATE TRIGGER trg_insert
AFTER INSERT
ON employees
FOR EACH ROW
EXECUTE FUNCTION log_message();
```

### Working

```sql
INSERT INTO employees
VALUES (101,'Rahul','IT',50000);
```

### Output

```text
New Record Inserted
```

---

# PROCEDURE vs FUNCTION

| Procedure | Function |
|------------|------------|
| Called using CALL | Called using SELECT |
| Return value optional | Must return value |
| Used for DB operations | Used for calculations |
| Can contain COMMIT/ROLLBACK | Cannot manage transactions |

---

# MOST IMPORTANT WINDOW FUNCTIONS

```sql
ROW_NUMBER()
RANK()
DENSE_RANK()
LEAD()
LAG()
SUM()
AVG()
COUNT()
```

---

# MOST IMPORTANT INTERVIEW QUESTION

### Difference Between CTE and View

| CTE | View |
|------|------|
| Temporary | Permanent |
| Exists for one query | Stored in database |
| Created using WITH | Created using CREATE VIEW |
| Improves readability | Reusable across queries |

### Difference Between Trigger and Procedure

| Trigger | Procedure |
|----------|----------|
| Executes automatically | Executes manually |
| Attached to table events | Called using CALL |
| INSERT/UPDATE/DELETE based | User controlled |
| Cannot be called directly | Can be called directly |

























