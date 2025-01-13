---
id: 1721254506-datetime-functions-in-sql
aliases:
  - Datetime Functions in SQL
tags: []
---

# Datetime Functions in SQL

### Introduction
Datetime functions in SQL are used for manipulating and formatting date and time values, providing several benefits:
- **Data manipulation**: Transform and format date and time values.
- **Querying and filtering**: Filter data based on specific time conditions.
- **Reporting and analysis**: Generate reports and perform time-based analysis.
- **Data consistency and integrity**: Validate and format date and time values.
- **Application development**: Efficiently handle time-related operations.
- **Collaboration and integration**: Work effectively with others and integrate SQL with other tools.

### Functions Specific to MySQL
#### CURRENT_DATE()
Retrieves the current date without the time component.
```sql
SELECT CURRENT_DATE() AS Current_date;
```
*Output:*
```
Current_date
------------
2023-06-26
```

#### NOW()
Retrieves the current date and time from the system.
```sql
SELECT NOW() AS Current_timestamp;
```
*Output:*
```
Current_timestamp
-------------------
2023-06-26 14:30:45
```

#### CURRENT_TIMESTAMP()
Retrieves the current date and time, similar to NOW().
```sql
SELECT CURRENT_TIMESTAMP() AS Current_timestamp;
```
*Output:*
```
Current_timestamp
-------------------
2023-06-26 14:30:45
```

### Universal SQL Datetime Functions
To explain these functions, we'll use the `Water_consumption_data_sa` table.

#### DAY(), MONTH(), and YEAR()
Extracts the day, month, or year portion from a date or timestamp.

- **DAY()**
  ```sql
  SELECT City, Date_recorded, DAY(Date_recorded) AS Day
  FROM Water_consumption_data_sa;
  ```

  *Output:*
  ```
  City          Date_recorded   Day
  -----------------------------------
  Johannesburg  2022-08-10      10
  Cape Town     2022-07-25      25
  Durban        2022-09-02      2
  Pretoria      2022-08-15      15
  Port Elizabeth2022-09-01      1
  Bloemfontein  2022-07-30      30
  ```

- **MONTH()**
  ```sql
  SELECT City, Date_recorded, MONTH(Date_recorded) AS Month
  FROM Water_consumption_data_sa;
  ```

  *Output:*
  ```
  City          Date_recorded   Month
  ------------------------------------
  Johannesburg  2022-08-10      8
  Cape Town     2022-07-25      7
  Durban        2022-09-02      9
  Pretoria      2022-08-15      8
  Port Elizabeth2022-09-01      9
  Bloemfontein  2022-07-30      7
  ```

- **YEAR()**
  ```sql
  SELECT City, Date_recorded, YEAR(Date_recorded) AS Year
  FROM Water_consumption_data_sa;
  ```

  *Output:*
  ```
  City          Date_recorded   Year
  -----------------------------------
  Johannesburg  2022-08-10      2022
  Cape Town     2022-07-25      2022
  Durban        2022-09-02      2022
  Pretoria      2022-08-15      2022
  Port Elizabeth2022-09-01      2022
  Bloemfontein  2022-07-30      2022
  ```

#### DATEDIFF()
Calculates the difference between two dates.
```sql
SELECT City, Date_recorded, DATEDIFF(DAY, Date_recorded, NOW()) AS Days_elapsed
FROM Water_consumption_data_sa;
```

*Output:*
```
City          Date_recorded   Days_elapsed
-------------------------------------------
Johannesburg  2022-08-10      320
Cape Town     2022-07-25      336
Durban        2022-09-02      297
Pretoria      2022-08-15      315
Port Elizabeth2022-09-01      298
Bloemfontein  2022-07-30      331
```

#### DATE_ADD()
Adds a specified interval to a date or datetime value.
```sql
SELECT City, Date_recorded, DATE_ADD(Date_recorded, INTERVAL 7 DAY) AS Next_review
FROM Water_consumption_data_sa;
```

*Output:*
```
City          Date_recorded   Next_review
-------------------------------------------
Johannesburg  2022-08-10      2022-08-17
Cape Town     2022-07-25      2022-08-01
Durban        2022-09-02      2022-09-09
Pretoria      2022-08-15      2022-08-22
Port Elizabeth2022-09-01      2022-09-08
Bloemfontein  2022-07-30      2022-08-06
```
