```javascript
Install
```

[follow this link to install](https://medium.com/yavar/install-and-configure-postgresql-and-pgadmin-on-ubuntu-20-04-22-04-52c52c249b9e)

# System

### Check status of the postgres

```bash
sudo systemctl status postgresql
```

### start / stop  / restart postgresql

```bash
sudo systemctl start postgresql
sudo systemctl stop postgresql
sudo systemctl restart postgresql
```

### start shell as a user

```bash
sudo -u postgres psql
```

# Basic

### list all databases

```sql
\list
```

### exit

```sql
q
```

### clear output of postgres

```sql
\clear
```

# Databases

### create a database

```sql
CREATE DATABASE TEST;
```

### list the databases

```sql
\l
# or
\list
# or
# pgadmin > databases > postgres > query tool
SELECT datname FROM pg_database;
```

### create the database

```sql
CREATE DATABASE TEST;
```

### change the database

```sql
\c TEST
```

### drop the database

```sql
DROP DATABASE TEST;
# just make sure to disconnect it from pgadmin
# pgadmin > databases > test >  disconnect
```

# CRUD

### create a table

```sql
CREATE TABLE person(
  id INT,
  name VARCHAR(100),
  city VARCHAR(100)
);
```

chevk at test > schema > public > tables > person

```sql
\d person
```

### Insert into table

```sql
INSERT INTO person 
(id, name, city)
VALUES
(102, 'raju', 'delhi'),
(103, 'parth', 'delhi'),
(104, 'jay', 'akola'),
(105, 'om', 'akola');
```

### Read the table

```sql
SELECT * FROM person
```

### Update the table

```sql
UPDATE person
SET city =  'Nashik'
WHERE id = 102
```

### Delete

```sql
DELETE FROM person
WHERE id = 101
```

# Data types

[see the datatypes in documentation](https://www.postgresql.org/docs/current/datatype.html)

# Constraints

### Primary key

```sql
PRIMARY KEY
```

### NULL constraint

```sql
NOT NULL
```

### Unique

```sql
UNIQUE
```

### Auto increment

```sql
SERIAL
```

### Default

```sql
DEFAULT
```

#### Example task

```sql
CREATE TABLE employee(
	emp_id SERIAL PRIMARY KEY,
	fname VARCHAR(50) NOT NULL,
	lname VARCHAR(50) NOT NULL,
	email VARCHAR(100) NOT NULL UNIQUE,
	dept VARCHAR(50),
	salary DECIMAL(10,2) DEFAULT 30000.00,
	hire_date DATE NOT NULL DEFAULT CURRENT_DATE
);
```

check it into terminal once

```sql
\d employee
```

insert some data

```sql
INSERT INTO employee
(emp_id, fname, lname, email, dept, salary, hire_date) 
VALUES
(1, 'Raj', 'Sharma', 'raj.sharma@example.com', 'IT', 50000.00, '2020-01-15'),
(2, 'Priya', 'Singh', 'priya.singh@example.com', 'HR', 45000.00, '2019-03-22'),
(3, 'Arjun', 'Verma', 'arjun.verma@example.com', 'IT', 55000.00, '2021-06-01'),
(4, 'Suman', 'Patel', 'suman.patel@example.com', 'Finance', 60000.00, '2018-07-30'),
(5, 'Kavita', 'Rao', 'kavita.rao@example.com', 'HR', 47000.00, '2020-11-10'),
(6, 'Amit', 'Gupta', 'amit.gupta@example.com', 'Marketing', 52000.00, '2020-09-25'),
(7, 'Neha', 'Desai', 'neha.desai@example.com', 'IT', 48000.00, '2019-05-18'),
(8, 'Rahul', 'Kumar', 'rahul.kumar@example.com', 'IT', 53000.00, '2021-02-14'),
(9, 'Anjali', 'Mehta', 'anjali.mehta@example.com', 'Finance', 61000.00, '2018-12-03'),
(10, 'Vijay', 'Nair', 'vijay.nair@example.com', 'Marketing', 50000.00, '2020-04-19');

SELECT * FROM employee
```

# Clauses

### Where

```sql
WHERE
```

### Distinct

```sql
DISTINCT
```

### Order by

```sql
ORDER BY
```

### Limit

```sql
LIMIT
```

### Like

```sql
LIKE
```

list all data in db

```rust
SELECT * FROM employee;
```

```sql
SELECT * FROM employee 
WHERE salary > 65000;

SELECT * FROM employee 
WHERE dept = 'IT'
OR dept = 'HR'
OR dept = 

SELECT * FROM employees 
WHERE 
salary >=40000 AND salary <=65000;
'Finance';
SELECT * FRSELECT * FROM employees 
WHERE 
salary BETWEEN 40000 AND 65000;OM employee 
WHERE dept IN ('IT', 'HR', 'Finance');

SELECT DISTINCT fname FROM employee;

SELECT * FROM employee ORDER BY fname;

SELECT * FROM employee LIMIT 3;

Select * FROM employee 
WHERE dept LIKE '%Acc%';

-- Starts with 'A': LIKE 'A%'
-- Ends with 'A': LIKE '%A'
-- Contains 'A': LIKE '%A%'
-- Second character is 'A': LIKE '_A%'
-- Case-insensitive contains 'john': ILIKE '%john%'
-- 2 charactor only 'john': ILIKE '__'
```

# Aggregate functions

### count

```sql
COUNT()
```

### sum

```sql
SUM()
```

### avg

```sql
AVG()
```

### minn

```sql
min()
```

### max

```sql
max()
```

bulk code

```sql
SELECT COUNT(*) FROM employees;

SELECT MAX(age) FROM employees;

SELECT MIN(age) FROM employees;

SELECT emp_id, fname, salary FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);

SELECT SUM(salary) FROM employees;
SELECT AVG(salary) FROM employees;
```

# Group By

```sql
SELECT dept FROM employees GROUP BY dept;

SELECT dept, COUNT(fname) FROM employees GROUP BY dept;
```

# String functions

```sql
-- concat
CONCAT(first_col, sec_col) 
CONCAT(first_word, sec_word, ...)

-- conact ws
CONCAT_WS('-', fname, lname)

-- substring
SELECT SUBSTRING('Hey Buddy', 1, 4);

-- replace
REPLACE(str, from_str, to_str)
REPLACE('Hey Buddy', 'Hey', 'Hello')

-- reverse
SELECT REVERSE('Hello World');

-- length 
Select LENGTH('Hello World');

-- upper and lower
SELECT UPPER('Hello World');
SELECT LOWER('Hello World');

-- left
SELECT LEFT('Abcdefghij', 3); 

-- right
SELECT RIGHT('Abcdefghij', 4); 

-- trim
SELECT TRIM('  Alright!  '); 

-- position
SELECT POSITION('OM' in ‘Thomas’); 
```

# Altering table

```sql
SELECT * FROM person;

-- simple
ALTER TABLE person
ADD COLUMN age INT;

-- add a default

ALTER TABLE person
DROP COLUMN age;

ALTER TABLE person
ADD COLUMN age INT DEFAULT 0;

-- rename
ALTER TABLE person
RENAME COLUMN name TO fname;

-- rename a table
ALTER TABLE contacts
RENAME TO mycontacts

RENAME TABLE contacts TO mycontacts;

-- change a column structure
ALTER TABLE person
ALTER COLUMN fname
SET DATA TYPE VARCHAR(200);

ALTER TABLE person
ALTER COLUMN fname
SET DEFAULT 'unknown';

ALTER TABLE person
ALTER COLUMN fname
DROP DEFAULT ;

-- check condidions
ALTER TABLE person
ADD COLUMN
mob varchar(15)
CHECK( LENGTH ( mob ) > 10 );

-- name a constraint
CREATE TABLE contacts1(
  name varchar(50),
  mob VARCHAR(15) UNIQUE,
  CONSTRAINT mob_no_less_than_10_digits CHECK ( LENGTH ( MOB ) > 10 );
)
```

Special cases

```sql
SELECT fname, salary,
  CASE 
    WHEN salary > 50000 THEN 'high' 
    ELSE 'low'
  END AS sal_cat
FROM employee;

SELECT fname, salary,
  CASE 
    WHEN salary > 50000 THEN 'high'
    WHEN salary > 30000 THEN 'mid'
    ELSE 'low'
  END AS sal_cat
FROM employee;

-- task : calculate bonus as 10 % of salary
SELECT fname, salary,
  CASE 
    WHEN salary > 0 THEN ROUND( salary / 10 )
    ELSE 0
  END AS sal_bonus
FROM employee;

-- task : tell number of emplyees taking salary ranges
SELECT 
  CASE 
    WHEN salary > 50000 THEN 'high'
    WHEN salary > 30000 THEN 'mid'
    ELSE 'low'
  END AS sal_cat,
  COUNT(*) AS total_employees_in_salary_category
FROM employee
GROUP BY 
  CASE 
    WHEN salary > 50000 THEN 'high'
    WHEN salary > 30000 THEN 'mid'
    ELSE 'low'
  END;
```

# Relationships

```sql
CREATE DATABASE store_db;
/c storedb;
```

create tables

```sql
CREATE TABLE customers (  
  cust_id SERIAL PRIMARY KEY, 
  cust_name VARCHAR(100) NOT NULL 
);

CREATE TABLE orders ( 
  ord_id SERIAL PRIMARY KEY, 
  ord_date DATE NOT NULL, 
  price NUMERIC NOT NULL,
  cust_id INTEGER NOT NULL, 
  FOREIGN KEY (cust_id) REFERENCES 
  customers (cust_id) 
);

INSERT INTO customers (cust_name)
VALUES 
    ('Raju'), ('Sham'), ('Paul'), ('Alex');
```

# Joins

```sql
-- inner join
SELECT cust_name FROM Customers c
INNER JOIN Orders o
on o.cust_id = c.cust_id
GROUP BY cust_name;

-- left join
SELECT cust_name FROM Customers c
LEFT JOIN Orders o
on o.cust_id = c.cust_id
GROUP BY cust_name;

-- right join
SELECT cust_name FROM Customers c
RIGHT JOIN Orders o
on o.cust_id = c.cust_id
GROUP BY cust_name;
```

