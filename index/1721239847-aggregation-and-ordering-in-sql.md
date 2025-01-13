---
id: 1721239847-aggregation-and-ordering-in-sql
aliases:
  - Aggregation and Ordering in SQL
tags:
  - #sql
---

# Aggregation and Ordering in SQL

Aggregation and ordering in SQL are essential for summarizing and arranging data, allowing us to analyze it from various perspectives. This involves combining multiple rows of data into single values (aggregation) and sorting the result set based on specified columns (ordering).

## Aggregation and Ordering
Aggregation refers to summarizing or combining multiple rows of data into a single value or set of values. Ordering refers to sorting the result set of a SQL query based on one or more columns.

### Aggregation Clauses
- GROUP BY: Groups the result set by one or more columns.
- HAVING: Filters the result set based on an aggregate function.
- ORDER BY: Sorts the result set based on the calculated values of the aggregates.

### Aggregate Functions
An aggregate function in SQL returns one value after calculating multiple values of a column. Common aggregate functions include `SUM()`, `AVG()`, `MAX()`, `MIN()`, and `COUNT()`.

- `GROUP BY`
The `GROUP BY` clause splits the data into meaningful groups, applies the aggregation function to each group, and combines the results into a new result set. It follows a split-apply-combine paradigm.
```sql
SELECT column1, FUNCTION(columnN)
FROM table_name
GROUP BY column1;
```

- `HAVING`
The `HAVING` clause is similar to the WHERE clause but is used to filter the result set based on an aggregate function. It is used after the GROUP BY clause.
```sql
SELECT column1, FUNCTION(columnN)
FROM table_name
GROUP BY column1
HAVING condition;
```

- `ORDER BY`
The `ORDER BY` clause is used to sort the result set based on the calculated values of the aggregations, either in ascending or descending order.
```sql
SELECT column1, FUNCTION(columnN)
FROM table_name
GROUP BY column1
ORDER BY FUNCTION(columnN) [ASC|DESC];
```

## Example Data

Consider a `Patient` table with the following data:
`Patient_id`	`Clinic_id`	`Age`
1	1	54
2	3	22
3	1	51
4	2	30
5	2	36
6	3	20
7	1	67
8	1	74
9	2	61
10	3	46

`GROUP BY` Illustration
- Split - Group records based on `Clinic_id`, creating distinct groups of patients belonging to each clinic.
- Apply - Calculate the average age of the patients within each clinic group using the AVG function.
- Combine - Retrieve the Clinic_id and corresponding average age, providing the average age for each clinic based on the grouped patients.
```sql
SELECT clinic_id, AVG(age)
FROM Patient
GROUP BY clinic_id;

/*
Result:
Clinic_id	AVG(Age)
1	61.5
2	42.33
3	29.33
*/
```

`HAVING` Example
Using the `HAVING` clause to filter results where the average age is greater than 30:
```sql
SELECT clinic_id, AVG(age)
FROM Patient
GROUP BY clinic_id
HAVING AVG(age) > 30;

/*
Result:
Clinic_id	AVG(Age)
1	61.5
2	42.33
*/
```

`ORDER BY` Example
Using the `ORDER BY` clause to sort the result set based on the average age in ascending order:
```sql
SELECT clinic_id, AVG(age)
FROM Patient
GROUP BY clinic_id
ORDER BY AVG(age) ASC;

/*
Result:
Clinic_id	AVG(Age)
3	29.33
2	42.33
1	61.5
*/
```
In conclusion, aggregation and ordering in SQL are powerful techniques for data summarization and organization, allowing for more insightful data analysis and reporting.
