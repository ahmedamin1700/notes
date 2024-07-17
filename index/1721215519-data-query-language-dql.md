---
id: 1721215519-data-query-language-dql
aliases:
  - Data Query Language (DQL)
tags:
  - #sql
---

# Data Query Language (DQL)

## Key DQL Statements
1. `SELECT` Multiple Columns - The `SELECT` statement retrieves data from one or more columns of a table. By specifying a comma-separated list of columns, you can retrieve data from specific columns in any order.

- Syntax

```sql
SELECT col1, col2, ...
FROM db.table_name;
```
- Example:

```sql
SELECT col1, col3
FROM db.Table_1;
```

2. `SELECT` All Columns - Using an asterisk `(*)` with `SELECT` retrieves all columns from a table.

- Syntax

```sql
SELECT * FROM db.table_name;
```
- Example:

```sql
SELECT * FROM db.Table_1;
```
3. `LIMIT` - The `LIMIT` clause restricts the number of rows returned in the results set.

- Syntax

```sql
SELECT * FROM db.table_name LIMIT number_of_rows;
```

- Example:

```sql
SELECT * FROM db.Table_1 LIMIT 2;
```
4. `SELECT DISTINCT` - The `SELECT DISTINCT` statement eliminates duplicate rows from the result set. It can be applied to one or more specific columns.

- Syntax

```sql
SELECT DISTINCT col1, col2, ...
FROM db.table_name;
```

- Example:

```sql
SELECT DISTINCT col3
FROM db.Table_2;
```
5. `DISTINCT` on Multiple Columns - When used with multiple columns, `DISTINCT` returns unique combinations of values across all the listed columns.

- Syntax

```sql
SELECT DISTINCT col1, col2, ...
FROM db.table_name;
```

- Example:

```sql
SELECT DISTINCT col1, col3
FROM db.Table_3;
```
6. `DISTINCT *` - Using `DISTINCT *` removes all rows that are exact duplicates from the results set.

- Syntax

```sql
SELECT DISTINCT * FROM db.table_name;
```
- Example:

```sql
SELECT DISTINCT *
FROM db.Table_3;
```

7. `WHERE` - The `WHERE` clause filters the results to include only the rows where a specific condition is true. It acts as a gatekeeper, deciding which rows from the original table meet the condition and should be included in the query result.

- Syntax

```sql
SELECT col1, col2, ...
FROM db.table_name
WHERE condition;
```
- Example:

```sql
SELECT *
FROM db.Table_4
WHERE col4 = 'value';
```

## Summary of SELECT Variants
- Multiple Columns: Retrieve data from specified columns.
```sql
SELECT col1, col2 FROM db.table_name;
```

- All Columns: Retrieve data from all columns.
```sql
SELECT * FROM db.table_name;
```

- `LIMIT`: Restrict the number of rows returned.
```sql
SELECT * FROM db.table_name LIMIT number_of_rows;
```

- `DISTINCT`: Eliminate duplicate rows.
```sql
SELECT DISTINCT col1 FROM db.table_name;
SELECT DISTINCT col1, col2 FROM db.table_name;
SELECT DISTINCT * FROM db.table_name;
```

- `WHERE`: Filter rows based on a condition.
```sql
SELECT * FROM db.table_name WHERE col1 = 'value';
```