## What is a Database?
Where we store the data in a organize way annd can be access easily.

## What is RDBMS?
where we can connect tables to each other and uses SQL for managing and querying data.

## SQL
Structured Query Language
Which is used to talk to our databases.

# Queries 
#### =>>SHOW ALL EXISTING DB
```javascript
SELECT datname FROM pg_database;
```

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

// PRIMARY KEY / DEFAULT /NOT NULL
CREATE TABLE person ( 
  id INT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  city VARCHAR(100) NOT NULL,
SALARY VARCHAR(100) NOT NULL DEFAULT = 25000
); 
```
  













