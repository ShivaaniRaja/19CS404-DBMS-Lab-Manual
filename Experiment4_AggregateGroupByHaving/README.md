# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to find how many employees have an income greater than 50K?

Table: employee
````sql
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
````

```sql
SELECT count(income>50000) as employees_count FROM employee
```

**Output:**

<img width="431" height="294" alt="image" src="https://github.com/user-attachments/assets/4ebaf768-f4d1-4bda-b71d-00d01d735b48" />

**Question 2**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits
````sql
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
````

```sql
SELECT name as fruit_name, min(inventory) as lowest_quantity FROM fruits
```

**Output:**

<img width="641" height="302" alt="image" src="https://github.com/user-attachments/assets/5e42186e-d41f-4ad3-a371-5d82f0c756fd" />


**Question 3**
---
Write a SQL query to  find the average salary of all employees?

Table: employee
````sql
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
````

```sql
select avg(income) as Average_Salary from employee

```

**Output:**

<img width="463" height="298" alt="image" src="https://github.com/user-attachments/assets/2e776f14-bfa8-400d-9355-7329fdd51295" />

**Question 4**
---
<img width="1023" height="246" alt="image" src="https://github.com/user-attachments/assets/d3ae21d4-d58d-443d-82f8-4cb5334ab899" />


```sql
SELECT Specialty,
       ROUND(AVG(TRUNC(MONTHS_BETWEEN(SYSDATE, DateOfBirth) / 12)), 2) AS AvgAge
FROM Doctors
GROUP BY Specialty;
```

**Output:**



**Question 5**
---
<img width="997" height="233" alt="image" src="https://github.com/user-attachments/assets/12dd83cb-81ad-4f4e-9215-d9858ac8bf13" />



```sql
SELECT substr(Date,1,7) AS Month,
        COUNT(RecordID) as TotalRecords
FROM MedicalRecords
GROUP By Month;
-- ORDER BY Month;
```

**Output:**
<img width="581" height="404" alt="image" src="https://github.com/user-attachments/assets/2402f3e6-416e-410b-b165-829afaa8fb6a" />


**Question 6**
---
<img width="968" height="223" alt="image" src="https://github.com/user-attachments/assets/d02d71df-df05-4750-8e8f-6f0e9e097195" />

```sql
SELECT Medication, avg(Dosage) AS AvgDosage
FROM Prescriptions
GROUP BY Medication;
```

**Output:**

<img width="606" height="733" alt="image" src="https://github.com/user-attachments/assets/fa338f9d-f59b-40b4-9376-91fbb1f701b6" />


**Question 7**
---
<img width="1165" height="252" alt="image" src="https://github.com/user-attachments/assets/92f0365b-5dc9-470c-801a-09db9951e823" />


```sql
SELECT (age/5)*5 AS age_group, MIN(salary) AS 'MIN(salary)' FROM customer1
GROUP BY age_group
HAVING MIN(salary)<2000;
```

**Output:**

<img width="581" height="316" alt="image" src="https://github.com/user-attachments/assets/cc0ec181-0137-49fc-b682-7ae1e2db6f73" />


**Question 8**
---
<img width="1171" height="288" alt="image" src="https://github.com/user-attachments/assets/7540d055-7654-435f-940e-e13e007e0ede" />


```sql
SELECT category_id, SUM(price*category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING Revenue>25;
```

**Output:**

<img width="572" height="424" alt="image" src="https://github.com/user-attachments/assets/7bb4b6ea-c631-44c3-89a9-f935612208fa" />


**Question 9**
---
<img width="1197" height="287" alt="image" src="https://github.com/user-attachments/assets/4e825a7a-c40c-4d02-97ac-1ce20623bd24" />


```sql
SELECT city, Sum(Income) as Income
FROM employee
GROUP BY city
HAVING Income>200000;

```

**Output:**

<img width="561" height="510" alt="image" src="https://github.com/user-attachments/assets/ed03ddef-b208-4f25-be74-eccf70d572f2" />


**Question 10**
---
<img width="1125" height="292" alt="image" src="https://github.com/user-attachments/assets/c54600a1-9c42-4b15-9418-a9b6bee32e79" />

```sql
SELECT category_id, MIN(price) AS Price
FROM products
GROUP BY category_id
HAVING Price<10;
```

**Output:**

<img width="569" height="348" alt="image" src="https://github.com/user-attachments/assets/f83135ba-e245-42d8-8e7f-7b688a669975" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
