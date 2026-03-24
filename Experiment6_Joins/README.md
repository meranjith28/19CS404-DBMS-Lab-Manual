# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
select c.cust_name from customer c left join orders o on c.customer_id=o.customer_id where o.purch_amt<100;
```

**Output:**

<img width="398" height="424" alt="image" src="https://github.com/user-attachments/assets/283844b4-5154-4e77-8370-2b22bb3209c9" />


**Question 2**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

```sql
select c.cust_name,
c.city,
o.ord_no,
o.ord_date,
o.purch_amt as "Order Amount"
from customer c left join 
orders o on c.customer_id=o.customer_id
order by o.ord_date asc;
```

**Output:**
<img width="1304" height="954" alt="image" src="https://github.com/user-attachments/assets/4b64e8af-367d-40b2-a149-f3fad95b7c4d" />


**Question 3**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

```sql
select o.ord_no,
o.purch_amt,
o.ord_date,
c.cust_name,
c.city as customer_city,
c.grade as grade,
s.name as salesman_name,
s.city as salesman_city,
s.commission
from orders o
inner join customer c 
on o.customer_id=c.customer_id
inner join salesman s
on c.salesman_id=s.salesman_id;
```

**Output:**
<img width="1287" height="595" alt="image" src="https://github.com/user-attachments/assets/f013cee8-d617-41f6-a818-0d5b9cc517a3" />


**Question 4**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.  

```sql
select o.ord_no,
o.purch_amt,
c.cust_name,
c.city
from orders o
inner join customer c
on o.customer_id=c.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**
<img width="1029" height="361" alt="image" src="https://github.com/user-attachments/assets/11afa5da-88d2-4527-b025-278d80ed4185" />


**Question 5**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

```sql
select c.cust_name as "Customer Name",
c.city,
s.name as Salesman,
s.commission
from customer c
inner join salesman s
on c.salesman_id=s.salesman_id
where s.commission>0.12;
```

**Output:**
<img width="1018" height="553" alt="image" src="https://github.com/user-attachments/assets/d9725e5d-04ac-4b8c-b6bd-60c092232a5e" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

```sql
select p.first_name,
s.surgery_id,
p.patient_id,
s.surgeon_id,
s.surgery_date
from PATIENTS p
inner join SURGERIES s
on p.patient_id=s.patient_id
where p.date_of_birth>'1990-01-01';
```

**Output:**

<img width="1309" height="311" alt="image" src="https://github.com/user-attachments/assets/babf6546-5f38-477f-b223-7990bc755b03" />


**Question 7**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column.

```sql
select s.name,c.cust_name,c.city,c.grade,c.salesman_id
from Salesman s
left join Customer c
on s.salesman_id=c.salesman_id;
```

**Output:**
<img width="1198" height="655" alt="image" src="https://github.com/user-attachments/assets/b2fd0af1-2fc7-4388-a981-90ce4a84da7c" />


**Question 8**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

```sql
SELECT
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM orders o
INNER JOIN customer c
    ON o.customer_id = c.customer_id
INNER JOIN salesman s
    ON o.salesman_id = s.salesman_id;


```

**Output:**
<img width="1345" height="836" alt="image" src="https://github.com/user-attachments/assets/fad93f28-a621-4e13-91b3-0fb67a5edaea" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

```sql
SELECT
    p.first_name
FROM patients p
INNER JOIN surgeries s
    ON p.patient_id = s.patient_id
WHERE s.surgery_date = '2024-01-15';


```

**Output:**

<img width="365" height="267" alt="image" src="https://github.com/user-attachments/assets/886d55d8-7d43-4d2d-b980-e9d8796454c5" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

```sql
SELECT
    p.first_name AS patient_name,
    t.*
FROM patients p
INNER JOIN test_results t
    ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';

```

**Output:**

<img width="1244" height="294" alt="image" src="https://github.com/user-attachments/assets/163c3a6a-9947-437a-83c0-559366f56f7d" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
