---
id: 1721247089-window-functions-syntax
aliases:
  - Window Functions Syntax
tags:
  - #sql
---

# Window Functions Syntax

It looks like you're delving into SQL window functions. Let's break down the key concepts and functions discussed in your notes.

### Window Functions in SQL
Window functions perform calculations across a set of table rows related to the current row. These functions can be used for various analytical operations like ranking, calculating running totals, and more.

#### Types of Window Functions
1. **Aggregate Functions**: Perform a calculation on a set of values and return a single value. Examples include:
   - `AVG()`
   - `MAX()`
   - `MIN()`
   - `SUM()`
   - `COUNT()`

2. **Ranking Functions**: Assign a rank to each row within a partition of a result set.
   - `ROW_NUMBER()`
   - `RANK()`
   - `DENSE_RANK()`
   - `NTILE()`

3. **Analytical Functions**: Perform calculations over a set of rows and return a single result for each row.
   - `LAG()`
   - `LEAD()`
   - `FIRST_VALUE()`
   - `LAST_VALUE()`

### Examples of Window Functions

#### 1. LEAD() Function
The `LEAD()` function accesses data from the next row in the result set. It is useful for comparing current rows with subsequent rows.

**Example:**
```sql
SELECT
    Department,
    First_name,
    Salary,
    LEAD(Salary, 1) OVER (
        PARTITION BY Department
        ORDER BY Date_started
    ) AS Next_salary
FROM
    Employee
ORDER BY
    Department;
```
- **Purpose**: To retrieve the salary of the next employee within the same department.
- **Result**: `Next_salary` column will contain the salary of the next employee based on the `Date_started`.

#### 2. FIRST_VALUE() Function
The `FIRST_VALUE()` function returns the first value in an ordered set of values.

**Example:**
```sql
SELECT
    Start_date,
    Department,
    First_name,
    FIRST_VALUE(First_name) OVER (
        PARTITION BY Department
        ORDER BY Start_date
    ) AS First_in_dept
FROM
    Employee
ORDER BY
    Department;
```
- **Purpose**: To find the first employee hired in each department.
- **Result**: `First_in_dept` column will contain the first employee's name in each department based on `Start_date`.

#### 3. LAST_VALUE() Function
The `LAST_VALUE()` function returns the last value in an ordered set of values.

**Example:**
```sql
SELECT
    Start_date,
    Department,
    First_name,
    LAST_VALUE(First_name) OVER (
        ORDER BY Start_date
    ) AS Last_employee
FROM
    Employee
ORDER BY
    Department;
```
- **Purpose**: To find the last employee hired.
- **Result**: `Last_employee` column will contain the last employee's name in the ordered result set.

#### 4. Aggregate Window Functions (e.g., MIN())
**Example:**
```sql
SELECT
    Department,
    First_name,
    Salary,
    MIN(Salary) OVER (
        PARTITION BY Department
    ) AS Min_salary
FROM
    Employee
ORDER BY
    Department;
```
- **Purpose**: To find the minimum salary in each department.
- **Result**: `Min_salary` column will show the minimum salary within each department.

#### 5. SUM() with Running Total
**Example:**
```sql
SELECT
    Department,
    First_name,
    Salary,
    SUM(Salary) OVER (
        PARTITION BY Department
        ORDER BY Date_Started
    ) AS Dept_salary_budget
FROM
    Employee
ORDER BY
    Department;
```
- **Purpose**: To calculate the running total of salaries in each department.
- **Result**: `Dept_salary_budget` column will show a running total of salaries ordered by `Date_Started`.

### Ranking Functions

#### 1. RANK()
**Example:**
```sql
SELECT
    First_name,
    Province,
    RANK() OVER (
        ORDER BY Province
    ) AS Rank_assign
FROM
    Employee
ORDER BY
    Province;
```
- **Purpose**: To rank employees based on `Province`.
- **Result**: Rows with the same `Province` value receive the same rank. Ranks are not consecutive if there are ties.

#### 2. DENSE_RANK()
**Example:**
```sql
SELECT
    First_name,
    Province,
    DENSE_RANK() OVER (
        ORDER BY Province
    ) AS Rank_assign
FROM
    Employee
ORDER BY
    Province;
```
- **Purpose**: Similar to `RANK()` but without gaps in the ranking sequence.
- **Result**: Consecutive ranks even if there are ties.

#### 3. ROW_NUMBER()
**Example:**
```sql
SELECT
    First_name,
    Province,
    ROW_NUMBER() OVER (
        PARTITION BY Province
        ORDER BY First_name
    ) AS Row_assign
FROM
    Employee
ORDER BY
    Province;
```
- **Purpose**: To assign a unique sequential number to each row within each `Province`.
- **Result**: Each row gets a unique number within its `Province`.

#### 4. NTILE()
**Example:**
```sql
SELECT
    First_name,
    Province,
    NTILE(2) OVER (
        PARTITION BY Province
        ORDER BY First_name
    ) AS Group_number
FROM
    Employee
ORDER BY
    Province;
```
- **Purpose**: To divide employees into two groups within each `Province`.
- **Result**: Each row gets a group number, dividing the partition into specified equal groups.

These examples cover the basics of using window functions in SQL to perform various analytical operations. Understanding these functions can greatly enhance your ability to manipulate and analyze data within SQL databases.