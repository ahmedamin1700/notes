---
id: 1721238535-numeric-functions-in-sql
aliases:
  - Numeric Functions in SQL
tags:
  - #sql  
---

# Numeric Functions in SQL

SQL Numeric Functions

Numeric functions are built-in operations in SQL that operate on numeric data types (such as integers, decimals, and floating-point numbers) and perform various mathematical and statistical operations on them.

## The Importance of Numeric Functions in SQL
- Data Manipulation: Allows for numerical data manipulation.
- Data Analysis: Facilitates data analysis by summarizing numerical datasets.
- Accuracy: Ensures accurate numerical data calculations.

## Introduction to Numeric Functions in SQL
### Types of Numeric Functions
##### Aggregate Numeric Functions:
- `MIN()`
- `MAX()`
- `AVG()`
- `SUM()`
- `COUNT()`
    
##### Scalar Numeric Functions:
- `ROUND()`
- `SQRT()`
- `LOG()`

## Examples of Numeric Functions
### The `MIN()` Function
returns the smallest or lowest value of the selected column.
```sql
SELECT MIN(Y_2020) AS Lowest_salary_2020
FROM Salaries.ghs_db;
```

### The `MAX()` Function
returns the largest or highest value of the selected column.
```sql
SELECT MAX(Y_2020) AS Highest_salary_2020
FROM Salaries.ghs_db;
```
### The `AVG()` Function
returns the average value of the selected numeric column.
```sql
SELECT AVG(Y_2022) AS Average_salary_2022
FROM Salaries.ghs_db;
```
### The `SUM()` Function
returns the total sum of a specified numeric column.
```sql
SELECT SUM(Y_2019) AS Total_salaries_2019
FROM Salaries.ghs_db;
```
### The `COUNT()` Function
returns the number of rows of a specified column.
```sql
SELECT COUNT(Province) AS Number_of_provinces
FROM Salaries.ghs_db;
```

### The `COUNT(DISTINCT column)` Function
returns the distinct or unique number of rows of a specified column.
```sql
SELECT COUNT(DISTINCT Province) AS Number_of_provinces
FROM Salaries.ghs_db;
```

### The `ROUND()` Function
rounds a numerical value to a specified number of decimal places.
```sql
SELECT ROUND(Y_2022, 2) AS Rounded_salaries
FROM Salaries.ghs_db
LIMIT 3;
```

### The `SQRT()` Function
returns the square root of a numerical value.
```sql
SELECT SQRT(Y_2021) AS Square_root_y_2021
FROM Salaries.ghs_db
LIMIT 3;
```

### The `LOG()` Function
returns the logarithm of a numeric value with a specified base.
```sql
SELECT LOG(Y_2021, 10) AS Log_y_2021
FROM Salaries.ghs_db
LIMIT 3;
```