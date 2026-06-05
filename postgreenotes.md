## What is a Database?
Where we store the data in a organize way annd can be access easily.

## What is RDBMS?
where we can connect tables to each other and uses SQL for managing and querying data.

## SQL
Structured Query Language
Which is used to talk to our databases.

### Some Important Queries in SQL SHELL
``` javascript
\l         - list all databases
\q         - quit
\c db_name - connect to database
\dt        - list all tables
\d tb_name - desc a table
\d+ tb_name- list all column
\! cls.    - list all column
```
#### IMPORTANT QUERY
``` javascript
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

``` javascript

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

``` javascript
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
``` javascript
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
``` java
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
``` java
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
``` java
SELECT fname, salary,
CASE WHEN salary >= THEN 'High' ELSE 'Low'
ENS AS sal_cat FROM employee/tb_name;


SELECT fname, salary,
CASE WHEN salary >=50000 THEN 'High'
WHEN salary BETWEEN 40000 AND 50000 THEN 'Mid' ELSE 'Low'
ENS AS sal_cat FROM employee/tb_name;
```






























