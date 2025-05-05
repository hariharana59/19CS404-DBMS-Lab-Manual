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
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700
```


```sql
CREATE TABLE item(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT,
    rate INTEGER,
    icom_id TEXT(4),
    foreign Key (icom_id) REFERENCES company(com_id)
    ON UPDATE SET NULL
    ON DELETE SET NULL
);
```

**Output:**
![Screenshot (162)](https://github.com/user-attachments/assets/4435ecec-311f-4e30-b46c-4f297033f65a)


**Question 2**
---
```
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           CustomerID  INTEGER     0                       0
1           Name        TEXT        0                       0
2           Email       TEXT        0                       0
3           JoinDate    DATETIME    0                       0
```

```sql
CREATE TABLE Customers(
    CustomerID INTEGER ,
    Name TEXT  ,
    Email TEXT ,
    JoinDate DATETIME
);
```

**Output:**
![Screenshot (163)](https://github.com/user-attachments/assets/f0ac9c67-bcd7-4be9-8f59-1f1a5b9467f0)


**Question 3**
---
```
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;
AttendanceID  EmployeeID  AttendanceDate  Status
------------  ----------  --------------  ----------
1             1           2024-08-01      Present
```

```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER primary key,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK(Status IN ('Present','Absent','Leave')),
    foreign key (EmployeeID) references Employees(EmployeeID)
);
```

**Output:**
![Screenshot (164)](https://github.com/user-attachments/assets/efd4d440-002e-4542-962d-c7e81b057465)


**Question 4**
---
```
Write an SQL command can to add a column named email of type TEXT to the customers table

 

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0
```

```sql
ALTER TABLE customers ADD COLUMN  email TEXT;
```

**Output:**
![Screenshot (165)](https://github.com/user-attachments/assets/681504b1-0879-415c-af54-bb1ed2afb929)

**Question 5**
---
```
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

 

 

For example:

Test	Result
INSERT INTO Student_details (RollNo, Name, Gender, Subject, email) 
VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');
select * from Student_details;
RollN  Name   Gen  Subject     email
-----  -----  ---  ----------  ----------------
1      John   M    Math        john@example.com
```

```sql
ALTER TABLE 'Student_details'ADD COLUMN email  TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**

![Screenshot (166)](https://github.com/user-attachments/assets/52ffb2ac-29c6-411c-bcc5-07fbabd52815)

**Question 6**
---
```
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.    
For example:

Test	Result
SELECT EmployeeID, Name, Position 
FROM Employee;
EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst
```


```sql
INSERT INTO Employee (EmployeeID,Name,Position)
VALUES(4,'Emily White','Analyst');
```

**Output:**
![Screenshot (167)](https://github.com/user-attachments/assets/c59c931c-64f5-4720-a7cc-89d7ccab246b)

**Question 7**
---
```
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed
```

```sql
CREATE TABLE ProjectAssignments(
    AssignmentID INTEGER primary key,
    EmployeeID INTEGER,
    ProjectID INTEGER ,
    AssignmentDate DATE NOT NULL,
    foreign key (EmployeeID) REFERENCES Employees(EmployeeID),
    Foreign key (ProjectID) REFERENCES Projects(projectID)
);
```

**Output:**
![Screenshot (168)](https://github.com/user-attachments/assets/7937af72-70d2-435c-868f-19e026ff2293)

**Question 8**
---
```
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851
```

```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished FROM Out_of_print_books;
```

**Output:**
![Screenshot (169)](https://github.com/user-attachments/assets/e13c4490-5142-4229-9783-851ffc4140f8)

**Question 9**
---
```
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science
```

```sql
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
    VALUES(205,'Olivia Green','F',NOT NULL,NOT NULL),
        (207  ,'Liam Smith','M ','Mathematics', 85),
        (208 ,'Sophia Johns',  'F','Science',NOT NULL);
```

**Output:**
![Screenshot (170)](https://github.com/user-attachments/assets/b5d75c1e-00a6-4209-a2a7-f0ee4c007dc7)

**Question 10**
---
```
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	Result
INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
SELECT * FROM contacts;
contact_id  first_name  last_name   email                 phone
----------  ----------  ----------  --------------------  ----------
1           John        Doe         john.doe@example.com  1234567890
```
```sql
CREATE TABLE contacts(
    contact_id INTEGER primary key,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK(LENGTH(Phone)>=10)
);
```

**Output:**
![Screenshot (171)](https://github.com/user-attachments/assets/194fc618-ca2b-4895-b477-b6e8bea73df4)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
