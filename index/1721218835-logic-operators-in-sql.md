---
id: 1721218835-logic-operators-in-sql
aliases:
  - Logic Operators in SQL
tags:
  - #sql
---

# Logic Operators in SQL

Logic operators combine, exclude, or negate conditions to evaluate the truth of a condition or a set of conditions.

- `OR` - Combines conditions and returns TRUE if any condition is TRUE.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col2 >= 25 
OR col3 = 'm';
```

- `AND` - Combines conditions and returns TRUE only if all conditions are TRUE.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col2 >= 20 
AND col3 = 'm';
```

- `IN` - Checks if a value in a column matches any value in a list.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col1 IN ('w', 'x', 'y');
```

- `BETWEEN` - Filters records within a specified range, inclusive of endpoints.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col2 BETWEEN 22 AND 50;
```

- `IS NULL` - Checks for NULL values in a column.
  - Example:
```sql
SELECT * 
FROM db.Table_3 
WHERE col2 IS NULL;
```

- `IS NOT NULL` - Checks for non-NULL values in a column.
  - Example:
```sql
SELECT * 
FROM db.Table_3 
WHERE col2 IS NOT NULL;
```

- `NOT` - Negates a condition.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col2 NOT BETWEEN 22 AND 50;
```

- `NOT IN` - Ensures a value does not match any value in a list.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE col1 NOT IN ('w', 'x', 'y');
```

- `LIKE` - Searches for a specified pattern in a text-based column using wildcards.
  - Example:
```sql
SELECT * 
FROM db.Table_2 
WHERE col1 LIKE '_a%';
```

Wildcards:
- `%`: Represents multiple characters.
  - Example: `South%` matches South Korea, Southern, etc.
- `_`: Represents a single character.
  - Example: `h_t` matches `hot`, `hat`, `hit`.

Order of Operations
- `()` evaluated first, then `AND`, and finally `OR`.
  - Example:
```sql
SELECT * 
FROM db.Table_1 
WHERE (col1 = 'w' OR col1 = 'x' OR col1 = 'y' OR col1 = 'z') 
AND col2 > 20;
```

By understanding and utilizing these logic operators effectively, you can construct complex queries to filter and manipulate data in your SQL databases.