---
id: 1721218036-comparison-operators-in-sql
aliases:
  - Comparison Operators in SQL
tags:
  - #sql
---

# Comparison Operators in SQL

When querying data, SQL provides various operators that can be used with the `WHERE` clause to filter data based on specific conditions. These operators are essential for comparing values and determining the truth or falsity of conditions.

## Common Comparison Operators

Here are some examples of comparison operators in SQL:
- **Equals (=)**: Checks if the value in a column is equal to a specified value.
- **Not Equals (<> or !=)**: Checks if the value in a column is not equal to a specified value.
- **Less Than (<)**: Checks if the value in a column is less than a specified value.
- **Greater Than (>)**: Checks if the value in a column is greater than a specified value.
- **Less Than or Equal To (<=)**: Checks if the value in a column is less than or equal to a specified value.
- **Greater Than or Equal To (>=)**: Checks if the value in a column is greater than or equal to a specified value.

## Using Comparison Operators with the `WHERE` Clause

- Equals `(=)` Operator
```sql
SELECT *
FROM db.Table_2
WHERE col1 = 'car';
```

- Not Equals `(<> or !=)` Operator
```sql
SELECT *
FROM db.Table_2
WHERE col1 <> 'car';
```

- Greater Than `(>)` Operator
```sql
SELECT *
FROM db.Table_2
WHERE col2 > 56;
```

- Less Than or Equal To `(<=)` Operator
```sql
SELECT *
FROM db.Table_2
WHERE col2 <= 56;
```

- Greater Than or Equal To `(>=)` Operator
```sql
SELECT *
FROM db.Table_2
WHERE col2 >= 56;
```

## Practical Uses of Comparison Operators

- Finding countries with a GDP greater than $400 billion:
```sql
SELECT *
FROM db.Countries
WHERE GDP > 400000000000;
```

- Finding global regions with a population less than 1 million:
```sql
SELECT *
FROM db.Regions
WHERE Population < 1000000;
```

- Finding development indexes after a certain date for a specific country:
```sql
SELECT *
FROM db.DevelopmentIndexes
WHERE Date > '2020-01-01' AND Country = 'SpecificCountry';
```

- Finding elder death rates for sub-Saharan countries during the COVID-19 crisis (between 2020 and 2023):
```sql
SELECT *
FROM db.DeathRates
WHERE Region = 'Sub-Saharan' AND Year BETWEEN 2020 AND 2023 AND AgeGroup = 'Elder';
```

By understanding and using these comparison operators effectively, you can filter and query your data in SQL to extract meaningful insights.