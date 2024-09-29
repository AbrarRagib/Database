# Database
Database notes


Database: 
No need to stablish any relation.
Relational Database: 
Must be connected one table to another table with a primary key.
Relations:
1.	One to one:
2.	One to many:
3.	Many to many: Need to add a junction table, for example when add two table we keep both table primary key as foreign key in junction table. 
Key:
1.	Primary key
2.	Composite key: two primary key merged. 
3.	Foreign key
Table values:
1.	Field: column
2.	Record: Raw
3.	Value: Data 
Sorting & Indexing:
Sorting:
1.	Ascending
2.	Descending 
Indexing: 
Indexing vs Sorting: Indexing creates an index file that consists of a list of rows in a logical row order, along with their corresponding physical position in the table. Sorting a table creates a separate table and fills it with data from the original table, in sorted order.
N.B. Indexing takes less space than sorting. When use sorting, a new file will be saved in the database which file have all the records. On the other hand, when we use indexing only link/ ID stored. 
DDL vs DML:
DDL stands for Data Definition Language and refers to SQL commands used to create, modify, and delete database structures such as tables, indexes, and views. DML stands for Data Manipulation Language and refers to SQL commands used to insert, update, and delete data within a database.
Query DDL:
SHOW DATABASES; -- shows all
CREATE DATABASE Test; -- create
DROP DATABASE TEST; -- Delete

Create table:
CREATE TABLE IPhone
(
    SERIAL int,
    SERIES varchar(15),
    PRICES DECIMAL(7,2),
    PRIMARY KEY(SERIES)
);

Insert values:
INSERT INTO IPhone (SERIAL, SERIES, PRICES)
VALUES 
(1, 'iPhone 12', 999.99),
(2, 'iPhone 13', 1099.99),
(3, 'iPhone 14', 1199.99);

Rename Table:
RENAME TABLE Iphone to NOKIA;

Delete:  
DROP TABLE NOKIA;


Query DML:
Viewing one column:
SELECT SERIES
FROM iphone; 
Viewing multiple column:
SELECT SERIES, PRICES
FROM iphone;

View whole table:
SELECT *
FROM iphone;

Remove Duplicate Values: 
SELECT DISTINCT PRICES
FROM iphone;

Set limit (Row wise):
SELECT *
FROM iphone
LIMIT 3;
----------
SELECT *
FROM iphone
LIMIT 3,4; -- set range (not show, how many lines will show)

Sorting:
SELECT *
FROM iphone
ORDER BY PRICES; -- ascending
---------------
SELECT *
FROM iphone
ORDER BY PRICES DESC; -- descending 
SELECT SERIAL, PRICES
FROM iphone
ORDER BY SERIAL, SERIES;

Arithmetic Operator in SQL:
SELECT 5+5;
SELECT 5/5;
SELECT 5*5;
SELECT 5%5;



Where:
SELECT SERIES
FROM iphone
WHERE PRICES=999.99; -- for string str=”test”
 ----------------

SELECT SERIES
FROM iphone
WHERE PRICES>=999.99;



AND:
SELECT SERIES, PRICES
FROM iphone
WHERE SERIAL BETWEEN 2 AND 5 

Not:
SELECT SERIES, PRICES
FROM iphone
WHERE SERIAL != 2;


OR:
SELECT *
FROM iphone
WHERE SERIAL = 5 or PRICES > 1000; -- WHERE SERIAL = 5 AND PRICES > 1000;
-------------------
SELECT *
FROM iphone
WHERE SERIAL=5 AND (SERIES='iPhone 16' or PRICES>=999);

Conditional Operator:
OR:
SELECT *
FROM iphone
WHERE SERIES IN ('iPhone 14','iPhone 15', 'iPhone 16');

AND NOT:
SELECT *
FROM iphone
WHERE SERIES NOT IN ('iPhone 14','iPhone 15', 'iPhone 16');

Like:
SELECT *
FROM iphone
WHERE SERIES LIKE 'i%'; -- match first digit here % means not nec to match 

------------------

SELECT *
FROM iphone
WHERE SERIES LIKE '%16'; -- match last digit

------------------------------
SELECT *
FROM iphone
WHERE SERIES LIKE '%1_'; -- here match 2nd last digit with iPhone 1_

AS keyword:
SELECT SERIES AS MODEL, PRICES AS 'DOLLER'
FROM iphone; 


Not null + Unique = primary key

Constraint, AUTO_INCREMENT:
CREATE TABLE Nokia
(
    ID INT NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(15) NOT NULL, -- not null must be provide data
    PRICE DOUBLE(10,2),
    SERIAL DOUBLE(10,2) UNIQUE, -- must be unique 
    PRIMARY KEY(ID)
);
INSERT INTO Nokia (NAME, PRICE, SERIAL)
VALUES 
('Nokia 3310', 49.99, 'SN12345'),
('Nokia 1100', 29.99, 'SN12346'),
('Nokia X', 199.99, 'SN12347');


Update table value:
UPDATE nokia
set PRICE=399
WHERE ID=2;

------------
UPDATE Table_Name
set Column_Name=Value
WHERE Primary_Key=value;
----------------------
UPDATE nokia
SET PRICE=PRICE+10
WHERE PRICE>50;

Delete:

DELETE FROM nokia
WHERE ID=1;
-----------
DELETE FROM nokia
WHERE ID>4;
Functions:
UPPER & LOWER:

SELECT UPPER(NAME)
FROM nokia;

------------

SELECT LOWER(NAME)
FROM nokia;

ConCat:

SELECT CONCAT(NAME,' is ','$',PRICE,' only')
FROM nokia;
-------

SELECT CONCAT(NAME,' is ','$',PRICE,' only') as Price_List
FROM nokia;

Gretest & Least:

SELECT GREATEST(3,4,5,6,7,8,9);
----------------

SELECT LEAST(3,4,5,6,7,8,9);
Power:
SELECT POW(2,3);
LOG:
SELECT LOG(2);
--------------
SELECT LOG10(2);

TRUNCATE:

SELECT TRUNCATE(3.1416,2);
---------
SELECT TRUNCATE(LOG(2),2);

Random:
SELECT RAND();

Exponential:
SELECT EXP(3);
Describe:
DESCRIBE nokia


Aggregate Functions in SQL: 
Takes many inputs but give only single output.
Count:
SELECT COUNT(*)
FROM nokia;
Max/Min:
SELECT MAX(PRICE)
FROM nokia;
-------------------
SELECT MIN(PRICE)
FROM nokia;
AVG & SUM:
SELECT SUM(PRICE),AVG(PRICE)
FROM nokia;	
-----------------
SELECT COUNT(*), MAX(ID),MIN(ID),SUM(ID),AVG(ID)
FROM nokia;


Subquery:
Create tables:
CREATE TABLE Employee(
    empid numeric(10),
    name varchar(20),
    salary numeric(10),
    department varchar(20)
);

CREATE TABLE Departments(
    deptid numeric(10),
    department varchar(20)
);


Incert values:
INSERT INTO Employee 
VALUES (100,"Jacob A",20000,"SALES"),(101,"James T",50000,"IT"),(102,"Riya S",30000,"IT");
INSERT INTO Departments 
VALUES (1,"IT"),(2,"ACCOUNTS"),(3,"SUPPORT");

MYSQL Subquery with WHERE Clause:
SELECT * 
FROM Employee 
WHERE department=(SELECT department FROM Departments WHERE deptid=1);

MYSQL Subquery with comparison operators:
Less than operator (<) 	
SELECT * 
FROM Employee 
WHERE salary < (SELECT avg(salary) from Employee)
Greater than or equal to operator (>=)
SELECT * 
FROM Employee 
WHERE salary >= (SELECT avg(salary) from Employee);
MYSQL Subquery with IN and NOT IN operators:
IN operator
SELECT * 
FROM Employee 
WHERE department IN (SELECT department FROM Departments);

Details: https://www.geeksforgeeks.org/mysql-subquery/ 

Need to leran from 35. Alter,update,group,
Statements:
ALTER statement in SQL:

Add new column:
ALTER TABLE nokia
ADD Review VARCHAR(20) – add new column

Change column Name:
ALTER TABLE nokia
CHANGE Review REVIEW VARCHAR(20);


Delete a column:
ALTER TABLE nokia
DROP COLUMN REVIEW;

Update Statement:

UPDATE nokia
SET REVIEW='Good'
WHERE id=2;
-------------
UPDATE nokia
SET REVIEW='Good'
WHERE id>2;

Group:
SELECT SERIAL,SUM(PRICE)
FROM nokia
GROUP BY SERIAL;
-----------
SELECT SERIAL,SUM(PRICE)
FROM nokia
GROUP BY SERIAL
ORDER BY SUM(PRICE) DESC;
TRUNCATE TABLE:
TRUNCATE TABLE nokia; -- delete only Table data




Join:
Supported Types of Joins in MySQL
INNER JOIN: Returns records that have matching values in both tables
LEFT JOIN: Returns all records from the left table, and the matched records from the right table
RIGHT JOIN: Returns all records from the right table, and the matched records from the left table
CROSS JOIN: Returns all records from both tables


