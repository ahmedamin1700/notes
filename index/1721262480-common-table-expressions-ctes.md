---
id: 1721262480-common-table-expressions-ctes
aliases:
  - Common Table Expressions (CTEs)
tags: []
---

# Common Table Expressions (CTEs) in SQL

## Data Overview
The following table, called `Employee`, contains information about employees in a company located in both Kenya and South Africa. The salary is recorded in US dollars.

| Start_date | First_name | Gender | Country      | Office       | Department     | Salary |
| ---------- | ---------- | ------ | ------------ | ------------ | -------------- | ------ |
| 2015-06-01 | Lily       | Female | South Africa | Johannesburg | Finance        | 1933   |
| 2020-08-01 | Gabriel    | Male   | Kenya        | Nairobi      | Marketing      | 1649   |
| 2022-03-01 | Maryam     | Female | Kenya        | Nairobi      | Data_analytics | 1995   |
| 2015-07-15 | Sophia     | Female | South Africa | Cape Town    | Data_analytics | 2497   |
| 2019-05-01 | Alex       | Male   | South Africa | Johannesburg | Data_analytics | 1957   |
| 2012-01-01 | Martha     | Female | Kenya        | Nairobi      | Finance        | 2622   |
| 2014-05-01 | Joshua     | Male   | South Africa | Cape Town    | Finance        | 1933   |
| 2017-06-15 | Emily      | Female | Kenya        | Kisumu       | Data_analytics | 2043   |
| 2016-01-01 | David      | Male   | South Africa | Johannesburg | Marketing      | 2276   |

## What are Common Table Expressions (CTEs)?

A Common Table Expression (CTE) is a named query that exists within the context of a larger query. Its results are temporarily stored such that they can be referenced later by other queries, other CTEs, or even itself. A CTE is only accessible within the larger query in which it is defined and will be lost as soon as the execution of this query is completed.

### CTE Syntax

```sql
WITH CTE_name (Column_list) AS (
    Query
)
SELECT Column_list
FROM CTE_name;
```

### Benefits of Using CTEs

CTEs improve code in several ways:

- **Readability:** CTEs allow us to break down complex queries into smaller, more intuitive logical parts that make the overall query easier to read and follow.
- **Maintainability:** CTEs help modularize queries, making it easier to change or update individual parts without affecting the entire query.
- **Reusability:** Once a CTE is defined, it can be referenced multiple times within the same query, eliminating the need to repeat subquery calculations.

### Example of CTE Usage

**Goal:** Compare the total salary with the average salary in each department.

#### CTE Definition

```sql
WITH Salary_totals AS (
    SELECT
        Department,
        SUM(Salary) AS Total_salary,
        COUNT(Department) AS No_Employees
    FROM
        Employees
    GROUP BY
        Department
)
SELECT
    Department,
    No_Employees,
    Total_salary,
    Total_salary / No_Employees AS Avg_salary
FROM
    Salary_totals;
```

#### Output

| Department     | No_Employees | Total_salary | Avg_salary |
| -------------- | ------------ | ------------ | ---------- |
| Finance        | 3            | 6488         | 2163       |
| Marketing      | 2            | 3925         | 1963       |
| Data_analytics | 4            | 8492         | 2123       |

### Example: Finding Longest-Serving Employee in Each Department

**Goal:** Find and award the longest-serving employee in each department.

#### CTE Definition

```sql
WITH Tenure_rank AS (
    SELECT
        Department,
        First_name,
        Start_date,
        RANK() OVER (
            PARTITION BY Department
            ORDER BY Start_date DESC
        ) AS Rank
    FROM
        Employees
)
SELECT
    Department,
    First_name,
    Start_date
FROM
    Tenure_rank
WHERE
    Rank = 1;
```

#### Output

| Department     | First_name | Start_date |
| -------------- | ---------- | ---------- |
| Finance        | Martha     | 2012-01-01 |
| Marketing      | David      | 2016-01-01 |
| Data_analytics | Sophia     | 2015-07-15 |

### Using Multiple CTEs

It is possible to specify more than one CTE within a single query. Each CTE definition is separated by a comma.

#### Example: Viewing Employees in Main Offices in Kenya and South Africa

```sql
WITH Main_office_employee_ke AS (
    SELECT
        Name,
        Gender,
        Department
    FROM
        Employees
    WHERE
        Country = 'Kenya' AND Office = 'Nairobi'
),
Main_office_employee_sa AS (
    SELECT
        Name,
        Gender,
        Department
    FROM
        Employees
    WHERE
        Country = 'South Africa' AND Office = 'Johannesburg'
)
SELECT *
FROM Main_office_employee_ke
UNION
SELECT *
FROM Main_office_employee_sa;
```

#### Output

| Name    | Gender | Department     |
| ------- | ------ | -------------- |
| Gabriel | Male   | Marketing      |
| Maryam  | Female | Data_analytics |
| Martha  | Female | Finance        |
| Lily    | Female | Finance        |
| Alex    | Male   | Data_analytics |
| David   | Male   | Marketing      |