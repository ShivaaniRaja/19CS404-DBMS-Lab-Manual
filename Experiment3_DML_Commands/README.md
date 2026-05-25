# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer
````sql
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
````

```sql
DELETE FROM Customer
WHERE(GRADE = 3 OR AGENT_CODE ='A008')
AND OUTSTANDING_AMT<5000;
```

**Output:**

<img width="1181" height="387" alt="image" src="https://github.com/user-attachments/assets/36711685-a533-47c7-bfea-3f9d1aedfa35" />


**Question 2**
---
Write a SQL query to find employees who were hired after January 1, 2020.
````sql
emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
````

```sql
SELECT * FROM emp
WHERE hiredate>'2020-01-01';
```

**Output:**

<img width="1174" height="339" alt="image" src="https://github.com/user-attachments/assets/3837d69d-48a8-47cb-8d03-b30762604a1b" />


**Question 3**
---
Show the categoryName and description from the categories table sorted by categoryName.
````sql
name                     type
---------------       ---------------
CategoryID           INTEGER
CategoryName     VARCHAR(25)
Description          VARCHAR(255)
````
```sql
SELECT CategoryName,Description FROM categories 
ORDER BY CategoryName;
```

**Output:**

<img width="1178" height="469" alt="image" src="https://github.com/user-attachments/assets/ea36b652-b371-4c92-aa85-5a3f1e24e27e" />


**Question 4**
---
Update the 'Selling_Price' to add 10% extra margin for all products supplied by the supplier with id 6.

PRODUCTS TABLE
````sql
name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
````

```sql
UPDATE PRODUCTS
SET sell_price = cast(sell_price * 1.10 as int)
WHERE supplier_id=6;
```

**Output:**

<img width="1174" height="467" alt="image" src="https://github.com/user-attachments/assets/696af29e-b629-4d6c-adc0-5c4912bee85f" />


**Question 5**
---
Write a SQL statement to show all the contact_name, address, city of all customers who are from 'Germany', 'Mexico' and 'Spain' countries.

customers table
````sql
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           CustomerID    INTEGER      0                       1
1           CustomerName  VARCHAR(50)  0                       0
2           ContactName   VARCHAR(50)  0                       0
3           Address       VARCHAR(50)  0                       0
4           City          VARCHAR(20)  0                       0
5           PostalCode    VARCHAR(10)  0                       0
6           Country       VARCHAR(15)  0                       0
````

```sql
SELECT ContactName,Address,City FROM customers
WHERE Country IN ('Germany','Mexico','Spain');
```

**Output:**

<img width="855" height="815" alt="image" src="https://github.com/user-attachments/assets/c3ccb658-9c2f-483c-b3d4-92816fb12d18" />


**Question 6**
---
Write a SQL query to determine the age group of value1 in the Calculations table as 'Child' if it is less than 13, 'Teen' if it is between 13 and 19, and 'Adult' if it is 20 or older.
````sql
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
````

```sql
SELECT id,value1, CASE
                    WHEN value1 <13 THEN 'Child'
                    WHEN value1 BETWEEN 13 AND 19 THEN 'Teen'
                    ELSE 'Adult'
                END AS age_group
            FROM Calculations;
```

**Output:**

<img width="756" height="294" alt="image" src="https://github.com/user-attachments/assets/a0868f9b-9538-4e0d-bcea-4f2cded96292" />


**Question 7**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE specialization IS NULL;

```

**Output:**

<img width="1172" height="1001" alt="image" src="https://github.com/user-attachments/assets/2e048f9e-1df9-4e87-afd0-80a96ae27d82" />


**Question 8**
---
 Write a SQL query to locate the details of customers with grade values above 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer
````sql
 customer_id |   cust_name    |    city    | grade | salesman_id

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
````
```sql
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer
WHERE grade>100;
```

**Output:**

<img width="1177" height="364" alt="image" src="https://github.com/user-attachments/assets/c19768f2-4aef-4029-93ff-d0f28b934c6d" />


**Question 9**
---
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id 

```sql
UPDATE employees
SET salary=salary*2
WHERE department_id=20
AND job_id LIKE '%MAN';
```

**Output:**

<img width="1178" height="273" alt="image" src="https://github.com/user-attachments/assets/31b95bd2-a238-4442-8d59-212c42ec1348" />


**Question 10**
---
<img width="946" height="448" alt="image" src="https://github.com/user-attachments/assets/b76adbba-1781-41ef-8610-d85f1473655f" />


```sql
SELECT name,city FROM salesman
WHERE CITY IN ('London','Rome');
```

**Output:**

<img width="626" height="352" alt="image" src="https://github.com/user-attachments/assets/9c712011-e507-46dd-b4e4-e47f20c62f53" />



## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
