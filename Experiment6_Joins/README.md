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
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

Customer Table:
![image](https://github.com/user-attachments/assets/fe81c85a-7862-41a6-b8e4-c976e31a7168)

Salesmen Table:
![image](https://github.com/user-attachments/assets/2176ba96-920d-4a25-934c-b8fd8a780851)


```sqlselect s.name from salesman s
left join customer c on s.salesman_id=c.salesman_id
where c.city="New York";
```

**Output:**

![image](https://github.com/user-attachments/assets/caac7df5-b81c-424d-a562-03ad9c7608fa)

**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

![image](https://github.com/user-attachments/assets/756b6972-c295-42b1-8048-2d6ca66d5031)


TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

![image](https://github.com/user-attachments/assets/7cee8afe-a071-4182-b22d-c225d155ab4b)

```sql
SELECT 
    p.first_name AS patient_name,
    t.*
FROM 
    patients p
INNER JOIN 
    test_results t
    ON p.patient_id = t.patient_id
WHERE 
    t.test_name = 'Blood Pressure';

```

**Output:**

![image](https://github.com/user-attachments/assets/84564edc-a102-4564-aa51-00584bf09981)


**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



DOCTORS TABLE:

ATTRIBUTES - doctor_id, first_name, last_name, specialization



```sql
select p.first_name as patient_name,d.first_name as doctor_name from patients p
inner join doctors d on p.doctor_id = d.doctor_id
where p.discharge_date is null;
```

**Output:**

![image](https://github.com/user-attachments/assets/5c030c56-7aaa-4015-b383-ac5e9ca0c4f9)


**Question 4**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city from customer c
inner join salesman s on c.salesman_id=s.salesman_id
where c.grade<300
order by c.customer_id asc;
```

**Output:**

![image](https://github.com/user-attachments/assets/18854a42-d2f0-4219-aef4-b89fa3dc3bed)


**Question 5**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT o.ord_no,o.ord_date,o.purch_amt,c.cust_name AS "Customer Name",c.grade,s.name AS "Salesman",s.commission FROM orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/e50d9b58-d76f-45a6-b4c1-0d60cdf4ec92)


**Question 6**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

```sql
select o.ord_no,o.purch_amt,c.cust_name,c.city from orders o
join customer c on o.customer_id=c.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**
![image](https://github.com/user-attachments/assets/460475a1-b2ee-4952-b1d1-ac3563ad7c3d)


**Question 7**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![image](https://github.com/user-attachments/assets/d46775f7-de66-46f6-bbe4-0a7ba9ad4d0b)



TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
![image](https://github.com/user-attachments/assets/43f89733-fab6-4662-9286-864ff0818fd6)


```sql
SELECT p.first_name AS patient_name,
       t.result_id,
       t.patient_id,
       t.test_name,
       t.result,
       t.test_date
FROM patients AS p
INNER JOIN test_results AS t ON p.patient_id = t.patient_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/e33e7681-c1fc-41db-9f37-498eef9f72c9)


**Question 8**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```sql
select c.cust_name as"Customer Name",c.city,s.name as Salesman,s.commission from customer c
join salesman s on c.salesman_id=s.salesman_id
where s.commission>0.12;
```
**Output:**

![image](https://github.com/user-attachments/assets/e2dcb700-96a7-41b9-a43f-a3cb86b7803e)


**Question 9**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

Customer Table:
![image](https://github.com/user-attachments/assets/3f57fa0f-9ce4-492f-9bc0-4678ef47e974)



Salesmen Table:

![image](https://github.com/user-attachments/assets/4234c018-9d50-4977-a7c3-847a2f5f4dbe)


```sql
SELECT s.name,
       c.cust_name,
       c.city,
       c.grade,
       c.salesman_id
FROM customer AS c
LEFT JOIN salesman AS s ON c.salesman_id = s.salesman_id
WHERE c.grade <= 100;
```

**Output:**

![image](https://github.com/user-attachments/assets/76b1cfeb-5498-43b2-bfc5-f0ef85919730)


**Question 10**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
select c.cust_name as "Customer Name",c.city,s.name as Salesman,s.city,s.commission from customer c
join salesman s on c.salesman_id=s.salesman_id
where s.commission>0.12 and c.city<>s.city;
```

**Output:**

![image](https://github.com/user-attachments/assets/8f940349-31d8-4d24-aba0-ef7e9e38aaf9)



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
