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
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
INSERT INTO Books (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished
FROM Out_of_print_books;
```

**Output:**

<img width="1242" height="377" alt="image" src="https://github.com/user-attachments/assets/ee9070f2-6924-4a79-8304-8f37d30e9aff" />

<img width="1227" height="377" alt="image" src="https://github.com/user-attachments/assets/299a844d-f1cc-4213-99c6-b57c81d3309d" />


**Question 2**
---
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

```sql
INSERT INTO Products (Name, Category, Price, Stock)
VALUES 
('Smartphone', 'Electronics', 800, 150),
('Headphones', 'Accessories', 200, 300);
```

**Output:**

<img width="1236" height="442" alt="image" src="https://github.com/user-attachments/assets/5d8f5efb-ed1d-4ad7-962e-c740d530abda" />

<img width="883" height="451" alt="image" src="https://github.com/user-attachments/assets/0b8cf9e7-6962-4423-a4c0-a19d930214b3" />


**Question 3**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

```sql
CREATE TABLE Orders (
    OrderID INTEGER,
    OrderDate TEXT,
    CustomerID INTEGER
);
```

**Output:**

<img width="1242" height="407" alt="image" src="https://github.com/user-attachments/assets/1bbdf9d6-9a03-42f3-a03d-035b9c754255" />


**Question 4**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.

```sql
INSERT INTO Customers (CustomerID, Name, Address)
VALUES (304, 'Peter Parker', 'Spider St');
```

**Output:**

<img width="1235" height="403" alt="image" src="https://github.com/user-attachments/assets/55b86059-4e27-4f7b-8ea2-ec79ccfaa188" />


**Question 5**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders (
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1242" height="365" alt="image" src="https://github.com/user-attachments/assets/d39fd3a9-18dd-44d2-9ff4-5dac73730b49" />

<img width="1236" height="357" alt="image" src="https://github.com/user-attachments/assets/3a94b44a-c3f1-4d05-bc67-e7b39dc7ac84" />

**Question 6**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK (Stock >= 0)
);
```

**Output:**

<img width="1238" height="408" alt="image" src="https://github.com/user-attachments/assets/d10063a6-2ea2-4b0e-8a28-f15e33666301" />

<img width="1233" height="397" alt="image" src="https://github.com/user-attachments/assets/61a51d8a-f1bd-42f5-acf2-162da2896399" />

**Question 7**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

```sql
ALTER TABLE employee ADD COLUMN department_id INTEGER;
ALTER TABLE employee ADD COLUMN manager_id INTEGER DEFAULT NULL;
```

**Output:**
<img width="1237" height="372" alt="image" src="https://github.com/user-attachments/assets/03eeec10-ef7e-4510-ab60-f2738fd4f227" />


<img width="1235" height="407" alt="Screenshot 2026-05-20 102600" src="https://github.com/user-attachments/assets/c41928cc-cb4f-4a05-bf79-de9dc52f0910" />


**Question 8**
---Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
CREATE TABLE Department (
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location TEXT
);
```

**Output:**


<img width="1226" height="367" alt="image" src="https://github.com/user-attachments/assets/69005597-ab92-4019-b56b-b49ac061d924" />


<img width="1240" height="367" alt="image" src="https://github.com/user-attachments/assets/7fc7bbef-c0da-433b-b0d1-5f9b4b0c82c6" />


**Question 9**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK (Amount > 0),
    DueDate DATE CHECK (DueDate > InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**


<img width="1237" height="455" alt="image" src="https://github.com/user-attachments/assets/330f700d-b649-4765-95cc-55e47a8d691f" />


<img width="1236" height="451" alt="image" src="https://github.com/user-attachments/assets/8afebb38-5e26-4a02-a95b-71cb324c7bdd" />

**Question 10**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```sql
ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;
```

**Output:**

<img width="1232" height="453" alt="image" src="https://github.com/user-attachments/assets/66f7934f-47fa-4267-adc3-f0c5afda492e" />

<img width="1230" height="450" alt="image" src="https://github.com/user-attachments/assets/a1a264b5-6b22-47d5-8659-a40ae98016b2" />

## SCREENSHOT OF MODULE 1 SEB COMPLETION GRADE


<img width="825" height="138" alt="image" src="https://github.com/user-attachments/assets/dcaaadd2-5879-4c87-9990-bfc5478953a3" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
