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
```
Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.

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
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, PHONE_NUMBER FROM EMPLOYEES WHERE EMPLOYEE_ID=105;
EMPLOYEE_ID  FIRST_NAME  SALARY      PHONE_NUMBER
-----------  ----------  ----------  ------------
105          David       8000        590.423.4569
```

```sql
update Employees 
set salary=8000
where employee_id=105 and salary <5000;
```

**Output:**
![Screenshot (172)](https://github.com/user-attachments/assets/eb05af14-4b92-41ac-9c9a-f545453a4c1e)


**Question 2**
---
```
Write a SQL statement to Change the supplier name to 'A1 Suppliers' where the supplier ID is 8 in the suppliers table.

Table info

suppliers(supplier_id,supplier_name,contact_person,phone_number,email,address)

For example:

Test	Result
select changes();
changes()
----------
1
```

```sql
update suppliers
set supplier_name="A1 Suppliers"
where supplier_id=8;
```

**Output:**

![Screenshot (173)](https://github.com/user-attachments/assets/cb9e581b-d013-4298-8e59-32cd585aca8a)

**Question 3**
---
```
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2
```

```sql
update products
set reorder_lvl=reorder_lvl*0.7
where cost_price>50 and quantity<100;
```

**Output:**
![Screenshot (174)](https://github.com/user-attachments/assets/a22dd864-15f2-4773-b086-627dba19c085)


**Question 4**
---
```
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
3           3           3           2024-03-25
```

```sql
update Employees
set email='not available',commission_pct=0.55
where department_id=110;
```

**Output:**
![Screenshot (175)](https://github.com/user-attachments/assets/1021f575-9991-463a-b1b9-9f3ee7bbc885)


**Question 5**
---
```
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
3           3           3           2024-03-25
```
```sql
delete from surgeries
where surgery_date='2024-02-28';
```

**Output:**

![Screenshot (176)](https://github.com/user-attachments/assets/bf45d38e-64ad-4959-8277-8507048132a9)

**Question 6**
---
```
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
```

```sql
delete from surgeries 
where Surgery_ID = 3;
```

**Output:**
![Screenshot (177)](https://github.com/user-attachments/assets/ce2d69a9-bd7a-4b98-9128-1e6e7da63957)

**Question 7**
---
```
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```

```sql
delete from Doctors
where specialization="Cardiology";

```

**Output:**
![Screenshot (178)](https://github.com/user-attachments/assets/6f711f8a-6cb5-43e2-83c0-c5a8a2d52a81)


**Question 8**
---
```
Write a SQL query to determine the age group of value1 in the Calculations table as 'Child' if it is less than 13, 'Teen' if it is between 13 and 19, and 'Adult' if it is 20 or older.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          value1      age_group
----------  ----------  ----------
1           10.0        Child
2           18.0        Teen
3           23.0        Adult
```

```sql
select id,value1, 
case
when  value1 <13 then"Child"
when value1 between 13 and 19 then "Teen"
else "Adult"
end as "age_group" from calculations;
```

**Output:**

![Screenshot (179)](https://github.com/user-attachments/assets/953c01c9-d629-4466-a0b1-aecc32283a9a)

**Question 9**
---
```
Write a SQL query to retrieve all orders where the purchase amount is between 500 and 4000 but exclude orders with purchase amounts of 948.50 and 1983.43. The query should return the columns: ord_no, purch_amt, ord_date, customer_id, and salesman_id.

Table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001
```


```sql
select ord_no,purch_amt,ord_date,customer_id ,salesman_id
from orders
where purch_amt between 500 and 4000 and purch_amt NOT IN (948.50,1983.43);
```

**Output:**
![Screenshot (180)](https://github.com/user-attachments/assets/7f6edb3a-8d6e-459d-af80-d2a6d6993f5c)


**Question 10**
---
```
Write a SQL query to find all employees who were hired in the year 2022 from emp table.

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
For example:

Result
empno       ename       job         mgr         hiredate    sal         comm        deptno
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
7369        SMITH       CLERK       7902        2022-08-22  800                     20
7499        ALLEN       SALESMAN    7698        2022-08-22  1600        300         30
7521        WARD        SALESMAN    7698        2022-08-22  1250        500         30
7900        JAMES       CLERK       7698        2022-08-22  950                     30
7902        FORD        ANALYST     7566        2022-08-22  3000                    20
7934        MILLER      CLERK       7782        2022-08-22  1300                    10
```

```sql
select empno,ename,job,mgr,hiredate,sal, comm,deptno
from emp
where hiredate between '2022-01-01' and '2022-12-31';
```

**Output:**
![Screenshot (181)](https://github.com/user-attachments/assets/aa460f04-4264-4436-a67f-00dad59c5e8a)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
