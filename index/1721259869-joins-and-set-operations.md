---
id: 1721259869-joins-and-set-operations
aliases:
  - Joins and set operations
tags: []
---

# Joins and set operations

### Set Operations
Set operations are used to combine the results of two or more SELECT queries. The rules for set operations are:
- Tables must have the same number of columns for comparison and combination.
- Columns used in set operations must have compatible data types.

#### **UNION**
Combines the results of two or more SELECT queries into a single result set, removing duplicates.
```sql
SELECT columns
FROM table1
UNION
SELECT columns
FROM table2;
```
- **Graphical Representation**: The combined area of both sets.

#### **INTERSECT**
Combines the results of two or more SELECT queries and returns only the rows that appear in all the result sets.
```sql
SELECT columns
FROM table1
INTERSECT
SELECT columns
FROM table2;
```
- **Graphical Representation**: The overlapping area of both sets.

#### **EXCEPT**
Retrieves the rows that appear in the first SELECT query but not in the second SELECT query. Used to find the difference between the results of two queries.
```sql
SELECT columns
FROM table1
EXCEPT
SELECT columns
FROM table2;
```
- **Graphical Representation**: The area of the first set that does not overlap with the second set.

### Joins
Joins are used to combine data from two or more tables based on a related column between them.

#### **INNER JOIN**
Returns only the rows from both tables where there is a match between the specified columns.
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```
- **Graphical Representation**: The overlapping area of both tables.

#### **LEFT JOIN (LEFT OUTER JOIN)**
Returns all the rows from the left table and only the matching rows from the right table.
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```
- **Graphical Representation**: All of the left table and the overlapping area with the right table.

#### **RIGHT JOIN (RIGHT OUTER JOIN)**
Returns all the rows from the right table and the matching rows from the left table.
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```
- **Graphical Representation**: All of the right table and the overlapping area with the left table.

#### **FULL OUTER JOIN**
Returns all the rows from both tables, including unmatched rows from both the left and right tables.
```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```
- **Graphical Representation**: All areas of both tables, including the overlapping and non-overlapping areas.

### Set Theory Basics
- **Set**: A collection of objects (elements).
- **Subset**: A set contained within another set.
- **Empty set**: A set with no elements (denoted by {}).

### Venn Diagrams
Venn diagrams are graphical representations used to illustrate logical relationships between sets (tables). Each set is represented by a circle, and the area inside the circle contains elements (records) of the set.
