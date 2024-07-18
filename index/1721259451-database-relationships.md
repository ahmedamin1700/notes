---
id: 1721259451-database-relationships
aliases:
  - Database relationships
tags: []
---

# Database relationships

### Database Keys
- **Primary Keys**: Uniquely identify each row in a table. They must contain unique values, cannot contain `NULL` values, and cannot be deleted unless the referencing constraint is removed.
  ```sql
  CREATE TABLE table_name (
      Column1 datatype(size) PRIMARY KEY,
      Column2 datatype(size),
      Column3 datatype(size)
  );
  ```

- **Foreign Keys**: Columns that create a link between data in two tables. They correspond to the primary key in another table and can contain `NULL` values and duplicates.
  ```sql
  CREATE TABLE table_name (
      Column1 datatype(size),
      Column2 datatype(size),
      Column3 datatype(size),
      FOREIGN KEY (Column1) REFERENCES table_name (column_name)
  );
  ```

- **Composite Keys**: Consist of two or more columns that together uniquely identify a row in a table.
  ```sql
  CREATE TABLE table_name (
      Column1 datatype(size),
      Column2 datatype(size),
      Column3 datatype(size),
      PRIMARY KEY (Column1, Column2)
  );
  ```

### Types of Relationships
- **One-to-One (1:1)**: An entity in one table relates to a maximum of one entity in another table.
- **One-to-Many (1:M)**: One entity in a table relates to multiple entities in another table and vice versa.
- **Many-to-Many (M:M)**: Entities in one table relate to multiple entities in another table, typically requiring a junction table to manage the relationship.

### Entity-Relationship Diagrams (ERDs)
ERDs are used to visually represent the structure of a database and its entities:
- **Conceptual Data Model**: Includes entities and cardinalities (relationships).
- **Logical Data Model**: Adds attributes to entities and relationships.
- **Physical Data Model**: Adds details like keys and data types.

### Example of Entities and Relationships
The example provided demonstrates relationships between `Customers`, `Products`, `Addresses`, and `Invoices` tables:

#### `Customers` Table
- `CustomerID`: integer(10)
- `Name`: varchar(255)
- `Age`: integer(255)
- `Occupation`: varchar(255)

#### `Products` Table
- `ProductID`: integer(10)
- `ProductDescription`: varchar(255)

#### `Addresses` Table
- `Primary Address`: varchar(255)
- `CustomerID`: integer(10)
- `EmployeeID`: integer(10)

#### `Invoices` Table
- `InvoiceID`: integer(10)
- `CustomerID`: integer(10)
- `ProductID`: integer(10)
- `Date`: date
- `Total`: integer(10)

These tables and relationships illustrate how entities in a database are interconnected through primary and foreign keys to ensure data integrity and efficient data management.
