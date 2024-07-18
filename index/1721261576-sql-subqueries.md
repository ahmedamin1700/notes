---
id: 1721261576-sql-subqueries
aliases:
  - SQL Subqueries
tags: []
---

# SQL Subqueries

### Introduction to Subqueries
- **Definition**: A subquery, or nested query, is a query within another SQL statement (e.g., SELECT, WHERE, FROM, JOIN, INSERT, UPDATE, DELETE).
- **Purpose**: Subqueries allow for data retrieval based on the results of an inner query, offering alternatives to JOINS, functions, and window functions.

### Subqueries in Practice
#### Example Dataset
- **Water_samples Table**: Contains sample names, purity scores, and analysis types.
- **Analysis_costs Table**: Lists costs for different analysis types.
- **Sample_location Table**: Provides locations and sources for each sample.

### Subqueries in the WHERE Clause
#### Use Case: Retrieve Samples with Above-Average Purity
1. **Calculate Average Purity**:
   ```sql
   SELECT AVG(Purity) FROM Water_samples;
   ```
2. **Use Subquery in WHERE Clause**:
   ```sql
   SELECT Sample_name
   FROM Water_samples
   WHERE Purity > (SELECT AVG(Purity) FROM Water_samples);
   ```

### Subqueries in the SELECT Clause
#### Example: Add Average Purity to Each Row
```sql
SELECT Sample_name, Purity,
  (SELECT AVG(Purity) FROM Water_samples) AS Avg_purity
FROM Water_samples;
```

### Correlated Subqueries
#### Use Case: Calculate Total Cost for Each Sample
1. **Setup Correlated Subquery**:
   ```sql
   SELECT ws_out.Sample_name, ws_out.Analysis_type,
     (SELECT Cost FROM Analysis_costs WHERE Analysis_type = ws_out.Analysis_type) AS Cost
   FROM Water_samples AS ws_out;
   ```

### Subqueries vs. JOINs
#### JOIN Equivalent for Cost Calculation
```sql
SELECT ws_out.Sample_name, ws_out.Analysis_type, an_cost.Cost
FROM Water_samples AS ws_out
JOIN Analysis_costs AS an_cost
ON ws_out.Analysis_type = an_cost.Analysis_type;
```

### Subqueries in FROM/JOIN Clauses
#### Derived Tables Example
1. **Intermediate Table with Costs**:
   ```sql
   SELECT ws_out.Sample_name, ws_out.Analysis_type,
     (SELECT Cost FROM Analysis_costs WHERE Analysis_type = ws_out.Analysis_type) AS Cost
   FROM Water_samples AS ws_out;
   ```
2. **Sum Costs**:
   ```sql
   SELECT SUM(Cost) AS Total_cost
   FROM (
     SELECT ws_out.Sample_name, ws_out.Analysis_type,
       (SELECT Cost FROM Analysis_costs WHERE Analysis_type = ws_out.Analysis_type) AS Cost
     FROM Water_samples AS ws_out
   ) AS Total_cost;
   ```

### Subqueries in WHERE/HAVING Clauses
#### Use Case: Filter Samples Based on Purity
1. **Subquery in WHERE Clause**:
   ```sql
   SELECT Sample_name, Purity
   FROM Water_samples
   WHERE Purity > (SELECT AVG(Purity) FROM Water_samples);
   ```
2. **Use Result in IN Clause**:
   ```sql
   SELECT Sample_name, Location, Source
   FROM Sample_location
   WHERE Sample_name IN (
     SELECT Sample_name
     FROM Water_samples
     WHERE Purity > (SELECT AVG(Purity) FROM Water_samples)
   );
   ```

### Summary
- **Subqueries**: Powerful for embedding queries, used for filtering, calculating, and transforming data.
- **Optimization Considerations**: While subqueries can simplify some tasks, they can also reduce readability and performance. Using JOINs where appropriate can be a clearer and often more efficient alternative.