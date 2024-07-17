---
id: 1721253809-miscellaneous-functions
aliases:
  - Miscellaneous Functions
tags: []
---

# Miscellaneous Functions

The document provides an overview of several SQL string, date, and miscellaneous functions. Here's a summary of the key points covered:

### CAST() Function
The `CAST()` function converts a value from one data type to another.

**Syntax:**
```sql
SELECT CAST(expression AS datatype) FROM Table_name;
```

**Example:**
```sql
SELECT D_O_B, CAST(D_O_B AS DATE) AS New_D_O_B FROM Household_individuals;
```
This converts `D_O_B` values from DATETIME to DATE.

### CONVERT() Function
The `CONVERT()` function is another way to convert data types.

**Syntax:**
```sql
SELECT CONVERT(value, datatype) FROM Table_name;
```

**Example:**
```sql
SELECT Weight, CONVERT(Weight, DECIMAL(4,2)) AS New_weight FROM Household_individuals;
```
This converts `Weight` values to DECIMAL(4,2).

### IFNULL() Function
The `IFNULL()` function returns an alternative value if the given expression is NULL.

**Syntax:**
```sql
SELECT IFNULL(expression, alternative_value) FROM Table_name;
```

**Example:**
```sql
SELECT Highest_ed, IFNULL(Highest_ed, 'No schooling') AS New_highest_ed FROM Household_individuals;
```
This replaces NULL values in `Highest_ed` with 'No schooling'.

### NULLIF() Function
The `NULLIF()` function returns NULL if two expressions are equal.

**Syntax:**
```sql
SELECT NULLIF(expression1, expression2) FROM Table_name;
```

**Example:**
```sql
SELECT Age, NULLIF(Age, 0) AS New_age FROM Household_individuals;
```
This converts `Age` values of 0 to NULL.

### ISNULL() Function
The `ISNULL()` function checks if an expression is NULL and returns 1 if true, otherwise 0.

**Syntax:**
```sql
SELECT ISNULL(expression) FROM Table_name;
```

**Example:**
```sql
SELECT Sex, Age, New_highest_ed FROM Household_individuals WHERE ISNULL(Ed_institution) = 1;
```
This filters rows where `Ed_institution` is NULL.

### COALESCE() Function
The `COALESCE()` function returns the first non-NULL value from a list of expressions.

**Syntax:**
```sql
SELECT COALESCE(expression1, expression2, expression3, ...) FROM Table_name;
```

**Example:**
```sql
SELECT Marital_status, Spouse_ID, Spouse, COALESCE(Spouse_ID, Spouse) AS New_spouse_ID FROM Household_individuals;
```
This combines `Spouse_ID` and `Spouse` to form `New_spouse_ID`, assigning 'N/A' if single or the spouse's ID if married.

### Data Overview
The provided table `Household_individuals` contains various attributes such as `ID`, `Sex`, `D_O_B`, `Age`, `Weight`, `Highest_ed`, `Ed_institution`, `Marital_status`, `Spouse`, and `Spouse_ID`. Each function is applied to this table to demonstrate its usage.

### Notes:
- Ensure that values are compatible with the target data type when using conversion functions.
- These functions help handle and manipulate NULL values effectively in SQL queries.