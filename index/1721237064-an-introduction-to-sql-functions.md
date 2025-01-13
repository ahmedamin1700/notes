---
id: 1721237064-an-introduction-to-sql-functions
aliases:
  - An Introduction to SQL Functions
tags:
  - #sql
---

# An Introduction to SQL Functions

## What are SQL Functions?
SQL Functions: Built-in operations for calculations, manipulations, or transformations on data.

### Advantages:
- Efficiency: Faster query execution times and improved performance.
- Reliability and Compatibility: Adherence to SQL standards across different platforms.
- Ease of Use: Ready-to-use without additional configuration.
- Extensive Functionality: Wide range of built-in functions for various operations.
- Portability: Standard functions allow for easy migration across database systems.
- Documentation and Built-in Support: Extensive documentation from database vendors.

### Syntax of SQL Functions
- General Syntax:
```sql
SELECT
  Column1,
  Function_name(Arguments) AS Named_result
FROM
  Database_name.Table_name
```

## Types of SQL Functions
### Numeric Functions:
Perform calculations on values and return numerical results.
- Examples: `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`, `POWER()`, `SQRT()`, `ROUND()`.

### String Functions:
Operate on string values for concatenation, manipulation, and formatting.
- Examples: `CONCAT()`, `LENGTH()`, `SUBSTRING()`, `UPPER()`, `LOWER()`.

### Conditional Flow Functions:
Allow conditional logic in SQL queries.
- Examples: `CASE()`, `IF()`, `IIF()`.

### Miscellaneous Functions:
Perform various tasks such as data type conversion and handling NULL values.
- Examples: `CONVERT()`, `CAST()`, `NULLIF()`, `IFNULL()`.

### Datetime Functions:
Handle date and time values for formatting, extraction, and manipulation.
- Examples: `CURRENT_DATE()`, `DATEADD()`, `FORMAT()`.

**Note**: Functions can work across different data types.

## How Functions Behave
### Aggregate Functions:
Summarize data at a column level, returning a single value.
- Examples: `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`.

### Scalar Functions:
Manipulate data at a row level, returning a single value for each row.
- Examples: `UPPER()`, `LOWER()`, `CONVERT()`, `CAST()`, `IF()`, `FORMAT()`.

### Window Functions:
A hybrid of aggregate and scalar functions.

## Example Data and Queries
- Dataset Example: South African Household Income and Expenditure Survey dataset (SAHIES).
- Table: Income_expenditure_2020
- Example: Find total income expenditure in the Free State province.

### Example Queries
- Aggregate Functions:
```sql
SELECT
  SUM(Free_state) AS Total_free_state
FROM
  Sahies.Income_expenditure_2020;
/*
Output:
Total_free_state = 38037
*/
```

- Multiple Aggregate Functions:
```sql
SELECT
  SUM(Western_cape) AS Total_spent_western_cape,
  SUM(Free_state) AS Total_spent_Free_state,
  AVG(Free_state)
FROM
  Sahies.Income_expenditure_2020;
/*
Output:
Total_spent_western_cape = 35895,
Total_spent_Free_state = 38037,
AVG(Free_state) = 12679.0000
*/
```

- Scalar Functions:
```sql
SELECT
  Expenditure_group,
  (Free_state - Northern_cape) AS Diff_fs_and_nc
FROM
  Sahies.Income_expenditure_2020;
/*
Output:
Expenditure_group: Housing, Diff_fs_and_nc: 4799
Expenditure_group: Recreation, Diff_fs_and_nc: 266
Expenditure_group: Transport, Diff_fs_and_nc: -3423
*/
```

- Using Functions Together:
```sql
SELECT
  SUM(Western_cape) AS Total_spent_western_cape,
  SUM(Northern_cape) AS Total_spent_northern_cape,
  ROUND(AVG(Free_state),0) AS Average_spent_free_state
FROM
  Sahies.Income_expenditure_2020;
/*
Output:
Total_spent_western_cape = 35895,
Total_spent_northern_cape = 36395,
Average_spent_free_state = 12679
*/
```

- SQL Functions Without Input Arguments
Examples:
- `RAND()`: Generates a random number between `0` and `1`.
- `CURRENT_DATE()`: Returns the current date.
```sql
SELECT
  CURRENT_DATE();
/*
Output:
CURRENT_DATE() = 2023-06-20
*/
```