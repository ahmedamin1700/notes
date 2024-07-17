---
id: 1721242155-window-functions-in-sql
aliases:
  - Window Functions in SQL
tags:
  - #sql
---

# Window Functions in SQL

## What are Window Functions?

Window functions in SQL extend the capabilities of standard aggregate functions, allowing for more detailed analysis without collapsing data into a summary format. They conduct operations across related row sets or "windows," enabling tasks like calculating running totals or finding maximum group values.

## Key Window Functions
- Aggregate Functions: `AVG()`, `MAX()`, `MIN()`, `SUM()`, `COUNT()`.
- Ranking Functions: `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()`.
- Analytical Functions: `LAG()`, `LEAD()`, `FIRST_VALUE()`, `LAST_VALUE()`

## Window Function Syntax

Window functions use data from specified row sets or windows, and the `PARTITION BY` and `ORDER BY` clauses can be used to define these windows and sort the data within them.
```sql
SELECT
    column1,
    ...,
    WIN_FUNCTION(arg) OVER (
        PARTITION BY columnX
        ORDER BY columnY
    )
FROM
    db_name.table_name;
```

Example 1: Using `PARTITION BY`

Suppose we have an Employee table with the following data:
Start_date  Department      Province        First_name  Gender	Salary
2015-06-01	Finance	        Gauteng	        Lily	    Female	35760
2020-08-01	Marketing	    Western Cape	Gabriel	    Male	30500
2022-03-01	Data Analytics	Free State	    Maryam	    Female	46200
2022-07-15	Marketing	    Gauteng	        Sophia	    Female	36900
2019-05-01	Data Analytics	Western Cape	Alex	    Male	36200
2012-01-01	Finance	        Free State	    Martha	    Female	48500
2014-05-01	Finance	Western Cape	        Joshua	    Male	35760
2017-06-15	Data Analytics	Gauteng	        Emily	    Female	37800
2016-01-01	Marketing	    Western Cape	David	    Male	31000

To compare each employee's salary with the average salary of their department:
```sql
SELECT
    Department,
    First_name,
    Salary,
    AVG(Salary) OVER (PARTITION BY Department) AS Average_salary
FROM
    Employee;

/*
Result:
Department	    First_name	Salary	Average_salary
Data Analytics	Emily	37800	40067
Data Analytics	Alex	36200	40067
Data Analytics	Maryam	46200	40067
Finance	        Joshua	35760	40007
Finance	        Lily	35760	40007
Finance	        Martha	48500	40007
Marketing	    David	31000	32800
Marketing	    Gabriel	30500	32800
Marketing	    Sophia	36900	32800
*/
```

Example 2: Using `ORDER BY`

To rank employees according to salary across the whole organization:
```sql
SELECT
    Department,
    First_name,
    Salary,
    RANK() OVER (ORDER BY Salary DESC) AS Rank
FROM
    Employee;

/*
Result:
Department	    First_name	Salary	Rank
Finance	        Martha	    48500	1
Data Analytics	Maryam	    46200	2
Data Analytics	Emily	    37800	3
Marketing	    Sophia	    36900	4
Data Analytics	Alex	    36200	5
Finance	        Lily	    35760	6
Finance	        Joshua	    35760	6
Marketing	    David	    31000	8
Marketing	    Gabriel	    30500	9
*/
```
Example 3: Combining `PARTITION BY` and `ORDER BY`

To rank employees in each department from lowest to highest salary:

```sql
SELECT
    Department,
    First_name,
    Salary,
    RANK() OVER (PARTITION BY Department ORDER BY Salary) AS Rank
FROM
    Employee;

/*
Result:
Department	    First_name	Salary	Rank
Data Analytics	Maryam	    46200	1
Data Analytics	Alex	    36200	2
Data Analytics	Emily	    37800	3
Finance	        Joshua	    35760	1
Finance	        Lily	    35760	1
Finance	        Martha	    48500	3
Marketing	    Sophia	    36900	1
Marketing	    David	    31000	2
Marketing	    Gabriel	    30500	3
*/
```
Example 4: Aggregate Window Functions with `ORDER BY`

To compare the average salaries for each department over time:

```sql
SELECT
    Start_date,
    Department,
    First_name,
    Salary,
    AVG(Salary) OVER (PARTITION BY Department ORDER BY Start_date) AS Average_salary
FROM
    Employee;

/*
Result:
Start_date	Department	    First_name	Salary	Average_salary
2012-01-01	Finance	        Martha	    48500	48500
2014-05-01	Finance	        Joshua	    35760	42130
2015-06-01	Finance	        Lily	    35760	40007
2016-01-01	Marketing	    David	    31000	31000
2020-08-01	Marketing	    Gabriel	    30500	30750
2022-07-15	Marketing	    Sophia	    36900	32800
2017-06-15	Data Analytics	Emily	    37800	37800
2019-05-01	Data Analytics	Alex	    36200	37000
2022-03-01	Data Analytics	Maryam	    46200	40033
*/
```
In summary, window functions enhance SQL's data analysis capabilities by enabling operations across related row sets while preserving individual row data within partitions. This allows for detailed and flexible analysis of data.
