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
```
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301
```
```sql
select * from customer s
where city<>(
select city 
from customer
order by id desc
)
```

**Output:**
![Screenshot (182)](https://github.com/user-attachments/assets/789e63a2-697f-418e-90e3-ea6e7b2d5919)


**Question 2**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000
```

```sql
select * from customers
where salary <2500;
```

**Output:**

![Screenshot (183)](https://github.com/user-attachments/assets/9874a64c-0d6a-4046-a0e7-ae4ba95d4210)

**Question 3**
---
```
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

For example:

Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85
```
```sql
select student_name,grade
from GRADES s
where grade=(
select min(grade)
from GRADES
where subject =s.subject
)
```
**Output:**

![Screenshot (184)](https://github.com/user-attachments/assets/9eb679bf-6ffc-48ed-ae7a-2f313b0daff0)

**Question 4**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
3           Kaushik     23          Kota        2000
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
6           Komal       22          Hyderabad   4500
7           Muffy       24          Indore      10000
```

```sql
select * from customers
where salary>1500;
```

**Output:**
![Screenshot (185)](https://github.com/user-attachments/assets/ee614aaa-ab9f-4bab-a568-1520a8c565e5)

**Question 5**
---
```
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002         5001
```

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM ORDERS o
JOIN SALESMAN s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';

```

**Output:**
![Screenshot (186)](https://github.com/user-attachments/assets/7511ff76-9aaa-40c1-b9b2-d9fbd27a1ca1)

**Question 6**
---
```
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.
Sample table: GRADES (attributes: student_id, student_name, subject, grade)
For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
2                Bob              Math             85
6                Frank            Science          85
7                John             Social           85
```
```sql
SELECT *
FROM GRADES g
WHERE (g.subject, g.grade) IN (
    SELECT subject, MIN(grade)
    FROM GRADES
    GROUP BY subject
);

```

**Output:**
![Screenshot (187)](https://github.com/user-attachments/assets/5da5cf10-6171-40ce-9a93-c695aef77b08)

**Question 7**
---
```
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)
For example:

Result
depar  department_name
-----  ---------------
5      Anesthesiologis
```

```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);

```

**Output:**

![Screenshot (188)](https://github.com/user-attachments/assets/dd4eddb3-03a5-4547-be3f-21618c602421)

**Question 8**
---
```
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
```
```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.commission = (
    SELECT MAX(commission)
    FROM salesman
);

```

**Output:**
![Screenshot (189)](https://github.com/user-attachments/assets/8e858e6f-10e5-41a9-a093-9812bd0c0b3b)


**Question 9**
---
```
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85
```

```sql
SELECT *
FROM GRADES g
WHERE (g.subject, g.grade) IN (
    SELECT subject, MAX(grade)
    FROM GRADES
    GROUP BY subject
);

```

**Output:**
![Screenshot (190)](https://github.com/user-attachments/assets/b69e894d-f478-4d2c-a10c-716e664e5174)


**Question 10**
---
```
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh
Employee Table
name             type
------------   ---------------
id                    INTEGER
name              TEXT
age                 INTEGER
city                 TEXT
income           INTEGER

For example:
Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
104    Obama            35               Florida          5000000
105    Linklon          32               Georgia          250000
107    Adam             35               California       5000000
```
```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**
![Screenshot (191)](https://github.com/user-attachments/assets/58fef6dc-536c-4088-947c-20bfc482d033)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
