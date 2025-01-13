---
id: 1721212666-data-definition-language-ddl
aliases:
  - Data Definition Language (DDL)
tags:
  - #sql
---

# Data Definition Language (DDL)

The data definition language (DDL) is a subset of SQL used to define, modify, and remove structures within a database, including tables, schemas, and other objects. DDL includes commands such as `CREATE TABLE`, `ALTER TABLE`, `TRUNCATE TABLE`, and `DROP TABLE`.

## Key Components of DDL
- Database Schemas and Tables:
    - Database Schema: A logical container for tables, providing a framework for organizing and managing them.
    - Tables: Fundamental building blocks of a database schema, storing data in rows and columns.

## DDL Commands
1. `CREATE DATABASE` - Used to create a new SQL database.

```sql
CREATE DATABASE database_name;
USE database_name;
```
Example:

```sql
CREATE DATABASE united_nations;
USE united_nations;
```
2. `CREATE TABLE` - Used to create new tables by specifying their structure, including columns and data types.

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype [Constraint],
    ...
);
```
Example:

```sql
CREATE TABLE Access_to_Basic_Services (
    id INT PRIMARY KEY,
    service_name VARCHAR(100) NOT NULL,
    availability BOOLEAN
);
```

3. Constraints - Constraints enforce rules on data in a table to maintain data integrity.
   - `NOT NULL`: Ensures that a column cannot have `NULL` values.
   - `PRIMARY KEY`: Uniquely identifies each row in a table, combining `NOT NULL` and `UNIQUE` constraints.
   - `UNIQUE`: Ensures all values in a column are unique.
   - `FOREIGN KEY`: Establishes a relationship between two tables.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

4. `ALTER TABLE` - Used to modify the structure of an existing table.

   - Add a column:

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

   - Delete a column:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

   - Rename a column:

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

   - Change the data type of a column:

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

Examples:

```sql
ALTER TABLE employees
ADD email VARCHAR(100);

ALTER TABLE employees
DROP COLUMN email;

ALTER TABLE employees
RENAME COLUMN last_name TO surname;

ALTER TABLE employees
MODIFY COLUMN salary DECIMAL(10, 2);
```

5. `TRUNCATE TABLE` - Used to remove all data from a table, effectively resetting it to an empty state. This operation is faster than deleting rows individually.

```sql
TRUNCATE TABLE table_name;
```

Example:

```sql
TRUNCATE TABLE Access_to_Basic_Services;
```

6. `DROP TABLE` and `DROP DATABASE` - Used to remove entire database objects such as tables or databases.

- Drop a table:

```sql
DROP TABLE table_name;
```

- Drop a database:

```sql
DROP DATABASE database_name;
```

Examples:

```sql
DROP TABLE Access_to_Basic_Services;
DROP DATABASE united_nations;
```

## Summary
- `CREATE DATABASE` and `USE`: Create and select a database.
- `CREATE TABLE`: Define new tables with specified columns and data types.
- Constraints: Enforce rules to maintain data integrity.
- `ALTER TABLE`: Modify existing tables by adding, deleting, renaming columns, or changing data types.
- `TRUNCATE TABLE`: Remove all data from a table.
- `DROP TABLE` and `DROP DATABASE`: Permanently delete tables or databases.
