# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

For example:

Test	Result
SELECT * FROM Student_details WHERE RollNo = 201;
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
201         David Lee   M           Physics     92

```sql
-- Insert Into Student_details(RollNo,Name,Gender,Subject,MARKS)
values(201,'David Lee','M','Physics',92);
```

**Output:**

![image](https://github.com/user-attachments/assets/b1bba3d7-1bd6-43db-a91f-0eb67b00b148)


**Question 2**
---
-- Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE
 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           name        varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           designatio  varchar(50  0                       0
6           net_salary  number      0                       0
7           dob         date        0                       0

```sql
-- ALTER TABLE Companies
ADD designation varchar(50);
ALTER TABLE Companies
ADD net_salary  number;
ALTER TABLE Companies
ADD dob date;



```

**Output:**

![image](https://github.com/user-attachments/assets/28437972-f768-47f2-af88-67f9dd2edb06)


**Question 3**
---
-- Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

For example:

Test	Result
pragma table_info('employees');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           name        TEXT        1                       0
2           salary      INTEGER     0                       0

```sql
ALTER TABLE Employees 
add salary INTEGER CHECK(salary>0);

```

**Output:**

![image](https://github.com/user-attachments/assets/0ca86aed-e2d9-4757-b40c-8a57be6d63ed)


**Question 4**
---
-- Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName

```sql
-- CREATE TABLE Employees(
EmployeeID INTEGER primary key,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary INTEGER CHECK(Salary>0),
DepartmentID INTEGER ,
FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID));
```

**Output:**

![image](https://github.com/user-attachments/assets/d4430d0c-2fed-43f1-a551-bbe6979e7bdd)

**Question 5**
---
-- Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0


```sql
-- CREATE TABLE Reviews(
ReviewID  INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

![image](https://github.com/user-attachments/assets/ce68afca-d684-495d-a600-67f0e63619ce)

**Question 6**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName

```sql
-- CREATE TABLE Products(
ProductID INTEGER primary key,
ProductName TEXT NOT NULL,
Price REAL CHECK(Price>0),
Stock INTEGER CHECK(Stock>=0)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/0971fa21-81d4-4cd3-ad54-41eb83581733)


**Question 7**
---
-- Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78
For example:

Test	Result
SELECT * FROM Student_details;
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202         Ella King   F           Chemistry   87
203         James Bond  M           Literature  78

```sql
-- INSERT INTO Student_details(RollNo,Name ,Gender,Subject,MARKS)
values(202,'Ella King','F','Chemistry',87),
(203,'James Bond','M','Literature',78);
```

**Output:**

![image](https://github.com/user-attachments/assets/0c93ff3f-1fad-4c7e-ac54-7f3ec0469215)

**Question 8**
---
-- Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1   

```sql
-- CREATE TABLE Orders(
OrderID INTEGER  primary key,
OrderDate DATE not NULL,
CustomerID INTEGER,
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) 

);
```

**Output:**

![image](https://github.com/user-attachments/assets/9086a847-5030-46a0-af82-f5b42a90be6a)

**Question 9**
---
-- Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0

```sql
--CREATE TABLE products(
product_id INTEGER primary key,
product_name TEXT not NULL,
list_price DECIMAL(10, 2) not NULL CHECK(list_price>=discount) CHECK(list_price>=0),
discount DECIMAL(10, 2) default 0 not NULL CHECK(discount>=0)
);
```

**Output:**

![Output9](output.png![image](https://github.com/user-attachments/assets/4f1ca4b2-873d-453e-b995-1348b675c19d)


**Question 10**
---
-- Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851
```sql
-- INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished)
SELECT *FROM Out_of_print_books ;
```

**Output:**

![image](https://github.com/user-attachments/assets/6e9c816f-e910-43e2-ab78-088d387859b8)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
