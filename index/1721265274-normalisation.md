---
id: 1721265274-normalisation
aliases:
  - Normalisation
tags:
  - #sql
---

# Normalisation

**Normalisation** is a database design technique used to organise data in a relational database. It reduces data redundancy and ensures data integrity by breaking down large, complex tables into smaller, related tables and establishing relationships between them. The process is guided by a set of rules and principles, often described using normal forms.

### Common Normal Forms:
1. **First Normal Form (1NF)**
2. **Second Normal Form (2NF)**
3. **Third Normal Form (3NF)**
4. Higher levels such as 4NF and 5NF

### Advantages of Normalisation:
1. **Data Integrity**: Reduces data redundancy and prevents anomalies during operations like insertion.
2. **Efficient Storage**: Leads to more efficient storage utilisation.
3. **Easier Maintenance**: Changes in data need to be updated in fewer places.
4. **Scalability**: Supports larger datasets with efficient indexing and data integrity.
5. **Flexible Querying**: Supports complex queries through table relationships.

### Disadvantages of Normalisation:
1. **Complex Design**: Designing and querying normalised databases can be complex due to multiple table joins.
2. **Performance**: Query performance may be slow, especially with complex joins and large datasets.
3. **Write Operations**: Normalised databases may struggle with write operations due to relationship overhead.
4. **Storage Overhead**: Maintaining primary and foreign keys adds storage overhead.
5. **Higher Normal Forms**: Can result in overly complex designs.

### Denormalisation
**Denormalisation** is a database design technique that intentionally introduces redundancy by combining tables or adding redundant data to one or more tables.

#### Advantages of Denormalisation:
1. **Faster Queries**: Redundant data offers faster query performance for complex queries and reporting.
2. **Simplified Schema**: Aids query development and maintenance, ideal for reporting and analytics.
3. **Read-Heavy Scenarios**: Prioritises faster queries over write complexities.
4. **Simpler SQL Queries**: Fewer joins result in simpler SQL queries and reduced performance issues.

#### Disadvantages of Denormalisation:
1. **Write Complexity**: Write operations can be slower and more complex due to redundancy.
2. **Data Integrity**: Ensuring consistent updates to redundant data is complex and error-prone.
3. **Increased Storage**: Consumes more storage space.
4. **Schema Management**: Managing schema changes becomes more challenging with increased database complexity.

### Data Anomalies
**Data anomalies** are unexpected occurrences in a dataset that can erode data accuracy, reliability, and usability.

#### Types of Data Anomalies:
1. **Update Anomaly**: Occurs when updating information requires modifying multiple rows, leading to inconsistencies if not done properly.
2. **Insertion Anomaly**: Occurs when a new record can't be added without introducing incomplete data.
3. **Deletion Anomaly**: Occurs when deleting data unintentionally removes necessary related data.

#### Prevention and Mitigation Strategies:
1. **Normalisation**
2. **Validation Rules**
3. **Data Entry Controls**
4. **Data Cleansing**
5. **Data Audits**
6. **Error-Handling Protocols**

### Key Normalisation Principles
1. **Atomic Values (1NF)**: Each column should contain only atomic (indivisible) values, eliminating repeating groups and ensuring data are stored in a tabular format.
2. **No Partial Dependencies (2NF)**: Non-key attributes should be fully functionally dependent on the entire primary key in a table with a composite primary key.
3. **No Transitive Dependencies (3NF)**: Non-key attributes should not depend on other non-key attributes within the same table.

### Normalisation in Practice:

**First Normal Form (1NF)**:
- **Criteria**: Atomicity, primary key, no duplicated rows or columns.
- **Example**:
  - Unnormalised: 
    ```
    Employee_id Name Job_codes Job_titles State_codes Home_states
    E001        Carmel J01, J02 Chef, Waiter 26, 26 Cape Town
    ```
  - 1NF: 
    ```
    Employee_id Name  Job_code Job_title State_code Home_state
    E001        Carmel J01      Chef      26         Cape Town
    E001        Carmel J02      Waiter    26         Cape Town
    ```

**Second Normal Form (2NF)**:
- **Criteria**: Already in 1NF, no partial dependencies.
- **Example**:
  - 1NF: 
    ```
    Employee_id Name  Job_code Job_title State_code Home_state
    E001        Carmel J01      Chef      26         Cape Town
    ```
  - 2NF (split into two tables): 
    ```
    Employee Table: 
    Employee_id Name  State_code Home_state
    E001        Carmel 26         Cape Town
    Job Table: 
    Employee_id Job_code Job_title
    E001        J01      Chef
    ```

**Third Normal Form (3NF)**:
- **Criteria**: Already in 2NF, no transitive dependencies.
- **Example**:
  - 2NF: 
    ```
    Employee Table: 
    Employee_id Name  State_code Home_state
    E001        Carmel 26         Cape Town
    ```
  - 3NF (split into two tables): 
    ```
    Employee Table: 
    Employee_id Name  State_code
    E001        Carmel 26
    State Table: 
    State_code Home_state
    26         Cape Town
    ```
