---
id: 1721255292-control-flow-functions-in-sql
aliases:
  - Control Flow Functions in SQL
tags: []
---

# Control Flow Functions in SQL

Sure, here's a summary of the content on control flow functions in SQL:

---

# Control Flow Functions in SQL

## Overview
Control flow functions are essential for implementing conditional logic and controlling the flow of execution within SQL queries. These functions allow for different actions or values to be returned based on specific conditions. Common control flow functions in SQL include the `IF` function and the `CASE` statement. These functions can be utilized in various SQL clauses such as `SELECT`, `UPDATE`, `WHERE`, `ORDER BY`, and `GROUP BY`.

## Data Overview
We use a table named `Households_individuals` containing information about individuals in households in Kenya from a 2020 survey.

### Sample Data
| ID   | Hh_ID | Sex    | Age | Weight | Schooling | Current_ed  | Marital_status | Spouse | Hhc_rship     |
|------|-------|--------|-----|--------|-----------|-------------|----------------|--------|---------------|
| 3901 | 2401  | Male   | 9   | 29.01  | Yes       | Class 3     | Single         | N/A    | Grandchild    |
| 3821 | 2789  | Male   | 22  | 67.00  | Yes       | Third year  | Single         | N/A    | Other relative|
| 3961 | 2233  | Female | 35  | 59.00  | Yes       | Masters     | Married        | Yes    | Partner       |
| 3741 | 2560  | Female | 14  | 45.22  | Yes       | Class 8     | Single         | N/A    | Child         |
| 3661 | 2934  | Male   | 69  | 77.00  | No        | N/A         | Married        | Yes    | NULL          |
| 3921 | 2006  | Female | 16  | 45.99  | Yes       | Form 2      | Single         | N/A    | Child         |

---

## IF() Function
The `IF()` function evaluates a condition and returns one value if the condition is TRUE and another if it is FALSE.

### Syntax
```sql
SELECT
    IF(condition, value_if_true, value_if_false)
FROM
    Table_name;
```

### Example
Assigning "Head" to `Hhc_rship` when its value is NULL:
```sql
SELECT
    ID,
    Hhc_rship,
    IF(ISNULL(Hhc_rship), 'Head', Hhc_rship) AS New_hhc_rship
FROM
    Household_individuals;
```

### Output
| ID   | Hhc_rship     | New_hhc_rship  |
|------|---------------|----------------|
| 3901 | Grandchild    | Grandchild     |
| 3821 | Other relative| Other relative |
| 3961 | Partner       | Partner        |
| 3741 | Child         | Child          |
| 3661 | NULL          | Head           |
| 3921 | Child         | Child          |

---

## CASE Statement
The `CASE` statement allows for multiple conditions leading to different actions. There are two types of CASE statements: Simple CASE and Searched CASE.

### Simple CASE
Compares a given expression to a set of values and returns the corresponding result.

#### Syntax
```sql
SELECT
    CASE Case_Expression
        WHEN value_1 THEN result_1
        ...
        ELSE result
    END AS Alias_name
FROM
    Table_name;
```

### Searched CASE
Evaluates a series of conditions and returns a result based on the first condition that evaluates to TRUE.

#### Syntax
```sql
SELECT
    CASE
        WHEN condition_1 THEN result_1
        ...
        ELSE result
    END AS Alias_name
FROM
    Table_name;
```

### Example
Categorizing individuals into age groups:
```sql
SELECT
    ID,
    Age,
    CASE
        WHEN Age <= 12 THEN '0-12'
        WHEN Age <= 19 THEN '13-19'
        WHEN Age <= 39 THEN '20-39'
        WHEN Age <= 59 THEN '40-59'
        ELSE '60+'
    END AS Age_group
FROM
    Household_individuals;
```

### Output
| ID   | Age | Age_group |
|------|-----|-----------|
| 3901 | 9   | 0-12      |
| 3821 | 22  | 20-39     |
| 3961 | 35  | 20-39     |
| 3741 | 14  | 13-19     |
| 3661 | 69  | 60+       |
| 3921 | 16  | 13-19     |

---

## Nested Conditional Statements
Nested conditional statements allow for more granular control and multiple levels of conditions.

### Nested IF Example
Categorizing education levels:
```sql
SELECT
    Schooling,
    Current_ed,
    IF(Current_ed IN ('PP1', 'PP2'), 'Pre-school',
        IF(Current_ed IN ('Class 1', 'Class 2', 'Class 3', 'Class 4', 'Class 5', 'Class 6', 'Class 7', 'Class 8'), 'Primary',
            IF(Current_ed IN ('Form 1', 'Form 2', 'Form 3', 'Form 4'), 'Secondary',
                IF(Current_ed IN ('First year', 'Second year', 'Third year', 'Fourth year', 'Fifth year', 'Sixth year', 'Masters', 'PHD'), 'Tertiary', 'Other')
            )
        )
    ) AS Ed_level
FROM
    Household_individuals
WHERE
    Schooling = 'Yes';
```

### Output
| Schooling | Current_ed  | Ed_level |
|-----------|-------------|----------|
| Yes       | Class 3     | Primary  |
| Yes       | Third year  | Tertiary |
| Yes       | Masters     | Tertiary |
| Yes       | Class 8     | Primary  |
| Yes       | Form 2      | Secondary|

---

### Nested IF and CASE Example
Categorizing individuals by age and gender:
```sql
SELECT
    Sex,
    Age,
    CASE
        WHEN age < 18 THEN IF(Sex = 'Female', 'Young female', 'Young male')
        ELSE IF(Sex = 'Female', 'Adult female', 'Adult male')
    END AS Age_category
FROM
    Household_individuals;
```

### Output
| Sex    | Age | Age_group   |
|--------|-----|-------------|
| Male   | 9   | Young male  |
| Male   | 22  | Adult male  |
| Female | 35  | Adult female|
| Female | 14  | Young female|
| Male   | 69  | Adult male  |
| Female | 16  | Young female|

---

This summary provides an overview of using control flow functions like `IF` and `CASE` to implement conditional logic in SQL queries. These examples demonstrate how to handle various data manipulations and classifications based on specific conditions.
