# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```


**Question 1**
--
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table
````sql
name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
````
```sql
SELECT grade, COUNT(*) 
FROM customer
WHERE grade > (
    SELECT AVG(grade)
    FROM customer
    WHERE city= 'New York'
)
GROUP BY grade;
```

**Output:**

<img width="544" height="328" alt="image" src="https://github.com/user-attachments/assets/6c1f1a2f-ae36-44b2-b7d3-3d1d5c299176" />


**Question 2**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE
````sql
name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)
````
ORDERS TABLE
````sql
name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
````

```sql
SELECT * FROM ORDERS
WHERE salesman_id IN (
    SELECT salesman_id
    FROM SALESMAN
    where city= 'New York'
);
```

**Output:**

<img width="1173" height="476" alt="image" src="https://github.com/user-attachments/assets/10a9b59a-62fa-493a-88be-22a578abac65" />


**Question 3**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

```sql
SELECT student_name, grade
FROM GRADES g1
WHERE grade = (
            SELECT min(grade)
            FROM GRADES g2
            WHERE g1.subject = g2.subject
)
```

**Output:**

<img width="758" height="412" alt="image" src="https://github.com/user-attachments/assets/bc596f94-4ce8-4bd8-90b6-3b0e2f8270c7" />

**Question 4**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer
````sql
name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
````

```sql
SELECT name,city
FROM customer
WHERE city IN(
            SELECT city
            FROM customer
            WHERE ID IN (3,7)
)
```

**Output:**

<img width="539" height="442" alt="image" src="https://github.com/user-attachments/assets/ad7ffbb2-235a-4a88-ba66-76421df3a8f7" />


**Question 5**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

```sql
SELECT *
FROM GRADES g
WHERE grade= (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject =g.subject
);
```

**Output:**
<img width="1176" height="434" alt="image" src="https://github.com/user-attachments/assets/06ebeb97-81c5-4069-871f-37cd3a3ad6dd" />


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS
````sql
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
````

```sql
SELECT * FROM CUSTOMERS
WHERE SALARY<2500
```

**Output:**
<img width="1182" height="448" alt="image" src="https://github.com/user-attachments/assets/b074e24c-c1af-4b71-90f8-bb024bb8ae96" />

**Question 7**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

```sql
SELECT o.ord_no,o.purch_amt,o.ord_date,o.customer_id,o.salesman_id
FROM Orders o
JOIN Salesman s
ON o.salesman_id=s.salesman_id
WHERE s.city='London';
```

**Output:**
<img width="1181" height="386" alt="image" src="https://github.com/user-attachments/assets/a0b2be9b-6cee-4e14-becc-04f7f47460a1" />


**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS
````sql
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
````

```sql
SELECT * FROM CUSTOMERS
WHERE AGE<30;
```

**Output:**

<img width="1180" height="570" alt="image" src="https://github.com/user-attachments/assets/96bc5867-840a-4971-83ff-def2f2e24163" />


**Question 9**
---
<img width="857" height="288" alt="image" src="https://github.com/user-attachments/assets/26a4470b-8863-4fac-b610-c887f574ff60" />


```sql
SELECT *
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);
```

**Output:**

<img width="862" height="390" alt="image" src="https://github.com/user-attachments/assets/e7abdffa-648a-48ad-bfb2-f654d0293f31" />


**Question 10**
---
rom the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table
````sql
name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)
````
customer table
````sql
name              type
-----------       ----------
customer_id   int
cust_name     text
city                text
grade            int
salesman_id  int
````
```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c
ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id)>1;
```

**Output:**

<img width="574" height="464" alt="image" src="https://github.com/user-attachments/assets/00b2aee2-d9ba-46ce-896d-64de7c1149cd" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
