---
id: 1721217173-querying-with-sql-useful-tools
aliases:
  - "Querying with SQL: Useful Tools"
tags:
  - #sql
---

# Querying with SQL: Useful Tools

When working with SQL, it’s often necessary to make result sets more readable or save results for future use. Here are two handy tools for achieving this: Aliasing and Saving Result Sets.

## Aliasing

Aliasing uses the AS keyword to temporarily rename columns or tables in a query. This can make complex column names simpler and more readable.

- Syntax for Aliasing

```sql
SELECT col_name_in_db AS new_col_name
FROM db.table;
```

## Notes on Aliasing
- Descriptive Names: Use descriptive aliases for clarity (e.g., first_name instead of name).
- `WHERE` Clause: You cannot use an alias in the `WHERE` clause of the same query.

## Saving a Result Set

To save the results of a query to a new or existing table, you can use the `INSERT INTO` statement. Instead of specifying `VALUES`, you can use a query to select the data to be inserted.
- Steps to Save a Result Set
  - Create a New Table: Define the structure of the table where the results will be saved.
  - Query the Data: Use a `SELECT` statement to retrieve the data you want to save.
  - Insert the Data: Use `INSERT INTO` to insert the queried data into the new table.

- Syntax for Saving a Result Set

```sql
INSERT INTO table_name (col_name(s))
SELECT col_name(s)
FROM db.table_name;
```
- Example of Saving a Result Set

  - Create a New Table:

```sql
CREATE TABLE Saved_table (
  Initials VARCHAR(255),
  Cost INT
);
```

  - Query the Data:

```sql
SELECT col1, col2
FROM db.Table_2;
```
  - Insert the Data:

```sql
INSERT INTO Saved_table (Initials, Cost)
SELECT col1, col2
FROM db.Table_2;
```
## Summary
- Aliasing: Use AS to make your query results more readable by renaming columns.
- Saving Result Sets: Use `INSERT INTO` combined with a `SELECT` statement to save query results to a new or existing table.

By incorporating these tools into your SQL queries, you can enhance readability and manage your data more efficiently.