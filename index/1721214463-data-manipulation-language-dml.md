---
id: 1721214463-data-manipulation-language-dml
aliases:
  - Data Manipulation Language (DML)
tags:
  - #sql
---

# Data Manipulation Language (DML)

Data Manipulation Language (DML) is a sublanguage of SQL that is used for manipulating data in a database.
The main DML statements include `INSERT`, `UPDATE`, and `DELETE`. 
These commands are used to add, edit, or delete data from database tables.

## Key DML Statements
1. `INSERT` - The `INSERT` statement is used to add new records to a database table. It allows you to insert new data into specific columns of a table by providing values that correspond to the column definitions.

- Syntax

```sql
INSERT INTO database_name.table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
- Example:

```sql
INSERT INTO Diabetes_care.Patient (First_name, Last_name)
VALUES ('Kennedy', 'Ngoma'), ('Mulenga', 'Mwamba');
```
In this example, two new records are inserted into the Patient table in the Diabetes_care database.

2. `UPDATE` - The `UPDATE` statement allows you to modify existing data within a database table. It only modifies the data in a table and does not alter its structure.

- Syntax

```sql
UPDATE database_name.table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
- Example:

```sql
UPDATE Diabetes_care.Clinic
SET Doses_available = 0
WHERE Clinic_name = 'Kasama';
```
In this example, the Doses_available column for the clinic named 'Kasama' is updated to 0.

3. `DELETE` - The `DELETE` statement is used to remove specific records from a database table. It allows for the precise removal of unwanted or outdated records based on specified conditions.

- Syntax

```sql
DELETE FROM database_name.table_name
WHERE condition;
```
- Example:

```sql
DELETE FROM Diabetes_care.Insulin
WHERE Expiry_year = '2022';
```
In this example, all records in the Insulin table where the Expiry_year is 2022 are deleted.

## Summary of DML Statements
- `INSERT`: Used to add new records to a database table. It specifies the table name, the columns to be inserted, and the corresponding values for each column.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

- `UPDATE`: Used to modify existing records in a database table. It specifies the table name, the columns to be updated, and the new values for each column.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
- `DELETE`: Used to remove records from a database table. It specifies the table name for the delete and the condition that should be true for the record to be deleted.

```sql
DELETE FROM table_name
WHERE condition;
```

**Important Note:** Always use the `WHERE` clause for selective updates and deletions to ensure that only the intended records are affected. Without a `WHERE` clause, all records in the table may be updated or deleted.
