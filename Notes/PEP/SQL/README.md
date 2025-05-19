# SQL Notes

## **Module 1: Database Theory**

### **What is a Database?**

A **database** is an organized collection of data that can be easily accessed, managed, and updated. Databases are used to store information in a structured way, making it possible to retrieve, insert, update, and delete data efficiently.

---

### **Key Characteristics of a Database**

1. **Structured Storage**:
    - Data is organized in tables, rows, and columns or other structures, depending on the database type.
2. **Efficient Data Access**:
    - Databases allow for quick and optimized querying using database management systems (DBMS).
3. **Scalability**:
    - Databases are designed to handle large amounts of data and support multi-user environments.
4. **Data Integrity**:
    - Enforces rules to maintain the accuracy and consistency of data.
5. **Security**:
    - Restricts access to authorized users and protects sensitive data.

---

### **Consistency in Databases**

**Consistency** refers to the accuracy, correctness, and validity of data within a database. It ensures that the database remains in a valid state according to defined rules and constraints, even after transactions or operations are performed.

---

#### **1. Types of Consistency**

##### **1.1 Database Consistency**

Ensures that the data adheres to the defined rules and constraints, such as:

- **Data Integrity Constraints**:
    - Primary keys must be unique.
    - Foreign keys must reference valid entries.
    - Fields must follow their specified data types.
- **Business Rules**:
    - Custom rules defined for application logic, such as an account balance not going negative.

##### **1.2 Transactional Consistency**

Ensures that the database transitions from one valid state to another after a transaction. If a transaction fails, the database must return to its previous valid state.

---

#### **2. Consistency in ACID Properties**

In the context of **ACID (Atomicity, Consistency, Isolation, Durability)** properties for transactions, **consistency** ensures that:

- Any transaction must bring the database from one valid state to another.
- The database must adhere to all constraints and rules throughout the transaction.

#### **Example**:

1. A bank transfer involves debiting one account and crediting another.
2. Constraints:
    - The sum of balances in all accounts must remain constant.
3. Consistency ensures:
    - Both debit and credit operations succeed together, or neither happens, preserving the constraint.

---

#### **3. Types of Consistency in Distributed Systems**

1. **Strong Consistency**:
    - After a write, all subsequent reads reflect the latest write.
    - Example: Relational databases (e.g., PostgreSQL).
2. **Eventual Consistency**:
    - All replicas converge to the same state eventually.
    - Example: NoSQL databases like DynamoDB, Cassandra.
3. **Causal Consistency**:
    - Ensures the order of related operations is preserved.
    - Example: If user A’s update is visible to user B, user A’s previous operations must also be visible.
4. **Read-Your-Writes Consistency**:
    - Ensures a user always sees their own updates immediately.

---

#### **4. Ensuring Consistency in a Database**

1. **Define Constraints**:
    - Use database constraints like `NOT NULL`, `UNIQUE`, `CHECK`, `PRIMARY KEY`, and `FOREIGN KEY`.
2. **Validate Transactions**:
    - Ensure business rules and database rules are enforced during transaction processing.
3. **Use ACID-Compliant Databases**:
    - Relational databases like MySQL, PostgreSQL, and Oracle ensure transactional consistency.
4. **Concurrency Control**:
    - Use mechanisms like locks or optimistic concurrency to ensure consistency in concurrent operations.
5. **Error Handling**:
    - Rollback transactions in case of errors or inconsistencies.

---

### **Introduction to RDBMS (Relational Database Management System)**

A **Relational Database Management System (RDBMS)** is a type of database management system that organizes data into **tables** with rows and columns. It is based on **relational theory** introduced by **Edgar F. Codd** in 1970 and uses **Structured Query Language (SQL)** for managing data.

---

#### **Key Concepts of RDBMS**

1. **Tables (Relations)**:
    - Data is stored in tables, which represent entities.
    - Each table has rows (records) and columns (attributes).
2. **Rows (Tuples)**:
    - Represent individual records in a table.
    - Example: A single customer in a "Customers" table.
3. **Columns (Attributes)**:
    - Represent properties or fields of the data.
    - Example: "Name", "Email", "Phone Number".
4. **Keys**:
    - **Primary Key**:
        - Uniquely identifies each row in a table.
    - **Foreign Key**:
        - Establishes relationships between tables by referencing a primary key in another table.
5. **Relationships**:
    - Define how tables are connected:
        - **One-to-One (1:1)**: Each row in one table relates to one row in another.
        - **One-to-Many (1:N)**: A row in one table relates to multiple rows in another.
        - **Many-to-Many (M:N)**: Multiple rows in one table relate to multiple rows in another (handled via junction tables).
6. **Schema**:
    - Defines the structure of the database, including tables, columns, data types, and constraints.
7. **SQL (Structured Query Language)**:
    - A standard language for querying and managing data in an RDBMS.

---

#### **Features of RDBMS**

1. **Data Integrity**:
    - Enforces rules like primary keys, foreign keys, and constraints to maintain accuracy.
2. **Data Consistency**:
    - Ensures that data is reliable and valid across transactions.
3. **Scalability**:
    - Handles large datasets efficiently.
4. **ACID Compliance**:
    - Ensures reliable transaction processing:
        - **Atomicity**: All or nothing.
        - **Consistency**: Database moves from one valid state to another.
        - **Isolation**: Transactions don’t interfere with each other.
        - **Durability**: Changes are permanent once committed.
5. **Multi-User Environment**:
    - Supports concurrent data access by multiple users.
6. **Data Security**:
    - Provides authentication, authorization, and encryption.
7. **Data Independence**:
    - Changes to the database structure don’t affect the applications using it.

---

## **Module 2: Data Modeling**

### **Database Schema**

A **schema** in a database is the blueprint or structure that defines how data is organized, stored, and managed. It acts as a logical container for objects like tables, views, indexes, and relationships in a database.

---

#### **1. Key Concepts of a Schema**

1. **Structure Definition**:
    - Specifies tables, columns, data types, and relationships.
2. **Logical Organization**:
    - Defines how the database objects relate to each other without detailing physical storage.
3. **Segmentation**:
    - In relational databases, a schema is often associated with a specific user or application.
4. **Data Integrity**:
    - Includes rules like constraints (e.g., PRIMARY KEY, FOREIGN KEY) to maintain valid and consistent data.

---

#### **2. Components of a Schema**

1. **Tables**:
    - Core objects where data is stored in rows and columns.
    - Example:
        
        ```sql
        CREATE TABLE Customers (
            CustomerID INT PRIMARY KEY,
            Name VARCHAR(50),
            Email VARCHAR(100)
        );
        
        ```
        
2. **Columns and Data Types**:
    - Define the attributes of a table and their data types.
    - Example: `CustomerID INT`, `Name VARCHAR(50)`.
3. **Relationships**:
    - Define how tables interact via **Primary Keys** and **Foreign Keys**.
    - Example:
        
        ```sql
        CREATE TABLE Orders (
            OrderID INT PRIMARY KEY,
            CustomerID INT,
            FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
        );
        
        ```
        
4. **Constraints**:
    - Rules that enforce data integrity.
        - `NOT NULL`: Ensures a column cannot have NULL values.
        - `UNIQUE`: Ensures all values in a column are unique.
        - `CHECK`: Validates data against a condition.
5. **Indexes**:
    - Improve query performance by enabling faster data retrieval.
    - Example:
        
        ```sql
        CREATE INDEX idx_customer_name ON Customers(Name);
        
        ```
        
6. **Views**:
    - Virtual tables based on the result of a query.
    - Example:
        
        ```sql
        CREATE VIEW CustomerOrders AS
        SELECT Customers.Name, Orders.OrderID, Orders.Total
        FROM Customers
        JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
        
        ```
        

---

#### **3. Types of Schemas**

1. **Logical Schema**:
    - Abstract design of the database.
    - Focuses on the structure, relationships, and rules.
    - Example: ER diagrams, table definitions, and constraints.
2. **Physical Schema**:
    - Specifies how data is physically stored on the disk.
    - Includes details like file storage, indexing, and partitioning.
3. **Application Schema**:
    - Subset of the logical schema used by specific applications or users.
    - Example: A schema dedicated to reporting tools.

---

### **Table Structure in PostgreSQL**

In PostgreSQL, a **table structure** defines the organization of data within a table. It includes the table name, columns, data types, constraints, and optional storage parameters.

---

#### **1. Basic Table Structure**

A PostgreSQL table consists of the following components:

1. **Table Name**:
    - The name of the table that uniquely identifies it in the database schema.
2. **Columns**:
    - Attributes of the table, each having a name and a data type.
3. **Data Types**:
    - Define the kind of data the column can hold (e.g., `INTEGER`, `VARCHAR`, `DATE`).
4. **Constraints**:
    - Rules to maintain data integrity (e.g., `PRIMARY KEY`, `NOT NULL`).
5. **Indexes**:
    - Optional structures to improve query performance.

---

#### **2. Creating a Table in PostgreSQL**

Use the `CREATE TABLE` statement to define a new table structure.

### **Syntax**:

```sql
CREATE TABLE table_name (
    column_name data_type [constraint],
    column_name data_type [constraint],
    ...
    [table_constraints]
);

```

---

#### **3. Example: Creating a Table**

#### **Customers Table**:

```sql
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,   -- Auto-incrementing primary key
    Name VARCHAR(100) NOT NULL,      -- Customer name cannot be NULL
    Email VARCHAR(255) UNIQUE,       -- Email must be unique
    PhoneNumber VARCHAR(15),         -- Optional phone number
    RegistrationDate DATE DEFAULT CURRENT_DATE -- Default value is today
);

```

---

#### **4. Key Components of a Table**

##### **4.1 Columns and Data Types**

Each column has a name and a data type that defines the type of data it can store.

| **Data Type** | **Description** | **Example** |
| --- | --- | --- |
| `INTEGER` | Whole numbers. | `100`, `-5` |
| `SERIAL` | Auto-incrementing integer (used for IDs). | `1`, `2`, `3` |
| `VARCHAR(n)` | Variable-length string with a maximum of `n` characters. | `'Hello'` |
| `TEXT` | Variable-length string (unlimited). | `'Lorem ipsum'` |
| `DATE` | Calendar date. | `2024-12-31` |
| `TIMESTAMP` | Date and time (without time zone). | `2024-12-31 14:30:00` |
| `BOOLEAN` | Boolean values. | `TRUE`, `FALSE` |

---

### **Normalization in Databases**

**Normalization** is a process in database design that organizes data to reduce redundancy and improve data integrity. It involves structuring tables and relationships to ensure data is stored efficiently, eliminating duplicate data and maintaining consistency.

---

#### **1. Objectives of Normalization**

1. **Eliminate Redundancy**:
    - Avoid storing the same data in multiple places.
2. **Ensure Data Integrity**:
    - Prevent anomalies during insert, update, or delete operations.
3. **Improve Query Performance**:
    - Simplify the structure for more efficient data retrieval.
4. **Maintain Consistency**:
    - Ensure data dependencies are logical and meaningful.

---

#### **2. Types of Anomalies Addressed by Normalization**

1. **Insertion Anomaly**:
    - Inability to add data without requiring unrelated data.
    - Example: Adding a new customer without an associated order.
2. **Update Anomaly**:
    - Changes in data require multiple updates, risking inconsistencies.
    - Example: Updating a customer’s address in multiple rows.
3. **Deletion Anomaly**:
    - Deleting a piece of data unintentionally removes related useful data.
    - Example: Deleting an order also removes the associated customer details.

---

#### **3. Normal Forms**

Normalization is achieved through a series of "normal forms." Each normal form builds on the previous one and introduces stricter rules.

##### **3.1 First Normal Form (1NF)**

A table is in **1NF** if:

1. Each column contains atomic (indivisible) values.
2. Each column contains values of a single type.
3. Each row is unique, with a unique identifier (primary key).

**Example (Not in 1NF)**:

| OrderID | CustomerName | Products |
| --- | --- | --- |
| 101 | Alice | Apples, Oranges |
| 102 | Bob | Bananas |
- **Problem**: The `Products` column contains multiple values.

**Solution (1NF)**:

| OrderID | CustomerName | Product |
| --- | --- | --- |
| 101 | Alice | Apples |
| 101 | Alice | Oranges |
| 102 | Bob | Bananas |

---

##### **3.2 Second Normal Form (2NF)**

A table is in **2NF** if:

1. It is in **1NF**.
2. All non-key attributes are fully dependent on the entire primary key (no partial dependency).

**Example (Not in 2NF)**:

| OrderID | ProductID | ProductName |
| --- | --- | --- |
| 101 | 1 | Apples |
| 101 | 2 | Oranges |
- **Problem**: `ProductName` depends only on `ProductID`, not the full composite key (`OrderID`, `ProductID`).

**Solution (2NF)**:

1. Split the table into two:
    - **Orders**:
        
        
        | OrderID | ProductID |
        | --- | --- |
        | 101 | 1 |
        | 101 | 2 |
    - **Products**:
        
        
        | ProductID | ProductName |
        | --- | --- |
        | 1 | Apples |
        | 2 | Oranges |

---

##### **3.3 Third Normal Form (3NF)**

A table is in **3NF** if:

1. It is in **2NF**.
2. All attributes are directly dependent on the primary key (no transitive dependency).

**Example (Not in 3NF)**:

| OrderID | CustomerID | CustomerName |
| --- | --- | --- |
| 101 | 1 | Alice |
| 102 | 2 | Bob |
- **Problem**: `CustomerName` depends on `CustomerID`, not directly on `OrderID`.

**Solution (3NF)**:

1. Split the table into two:
    - **Orders**:
        
        
        | OrderID | CustomerID |
        | --- | --- |
        | 101 | 1 |
        | 102 | 2 |
    - **Customers**:
        
        
        | CustomerID | CustomerName |
        | --- | --- |
        | 1 | Alice |
        | 2 | Bob |

---

#### **4. Advantages of Normalization**

1. **Reduces Redundancy**:
    - Minimizes duplicate data.
2. **Improves Data Integrity**:
    - Prevents inconsistencies during updates or deletions.
3. **Efficient Storage**:
    - Optimizes database size.
4. **Better Maintenance**:
    - Simplifies updates to the schema.

---

#### **5. Disadvantages of Normalization**

1. **Complex Queries**:
    - Requires multiple joins for retrieving data from related tables.
2. **Performance Overhead**:
    - Joins can slow down read operations in very large datasets.
3. **Not Ideal for Analytics**:
    - De-normalized structures are better suited for OLAP systems.

---

#### **6. When to Normalize**

- Use normalization for OLTP (Online Transaction Processing) systems where data integrity and efficiency are critical.
- Consider de-normalization for OLAP (Online Analytical Processing) systems to optimize read-heavy operations.

---

### **Multiplicity in Database Relationships**

**Multiplicity** defines the number of entities that can be associated with another entity in a relationship. It is a concept from **Entity-Relationship Modeling (ERD)** and is used to represent cardinality in database design.

---

#### **1. Types of Multiplicity**

Multiplicity is expressed in terms of **cardinality**, which can be classified into three main types:

##### **1.1 One-to-One (1:1)**

- **Definition**: Each entity in Table A is related to exactly one entity in Table B, and vice versa.
- **Example**: A **User** has one **Profile**, and a **Profile** belongs to one **User**.

**Schema**:

```sql
CREATE TABLE Users (
    UserID SERIAL PRIMARY KEY,
    Username VARCHAR(50)
);

CREATE TABLE Profiles (
    ProfileID SERIAL PRIMARY KEY,
    UserID INT UNIQUE,
    Bio TEXT,
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);

```

**Use Case**:

- User accounts and their profile details.
- Passport and its associated citizen.

---

##### **1.2 One-to-Many (1:N)**

- **Definition**: An entity in Table A can be related to multiple entities in Table B, but each entity in Table B relates to only one entity in Table A.
- **Example**: A **Customer** places multiple **Orders**, but each **Order** belongs to one **Customer**.

**Schema**:

```sql
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,
    Name VARCHAR(100)
);

CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```

**Use Case**:

- Customers and their orders.
- Teachers and their students.

---

##### **1.3 Many-to-Many (M:N)**

- **Definition**: Entities in Table A can relate to multiple entities in Table B, and entities in Table B can relate to multiple entities in Table A.
- **Example**: **Students** can enroll in multiple **Courses**, and **Courses** can have multiple **Students**.

**Schema**:

1. Create a junction table to establish the relationship.

```sql
CREATE TABLE Students (
    StudentID SERIAL PRIMARY KEY,
    Name VARCHAR(100)
);

CREATE TABLE Courses (
    CourseID SERIAL PRIMARY KEY,
    CourseName VARCHAR(100)
);

CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

```

**Use Case**:

- Students and courses.
- Products and categories.

---

#### **2. Cardinality Notations in ERD**

In Entity-Relationship Diagrams (ERD), multiplicity is represented using specific notations:

| **Notation** | **Description** | **Example** |
| --- | --- | --- |
| `1:1` | One-to-One relationship. | User ↔ Profile |
| `1:N` | One-to-Many relationship. | Customer → Orders |
| `M:N` | Many-to-Many relationship. | Students ↔ Courses |

---

#### **3. Real-World Examples of Multiplicity**

##### **3.1 Banking System**

- **One-to-One**: Account ↔ Customer Details
- **One-to-Many**: Customer → Transactions
- **Many-to-Many**: Customers ↔ Accounts (e.g., joint accounts)

##### **3.2 E-Commerce**

- **One-to-One**: Order ↔ Invoice
- **One-to-Many**: Customer → Orders
- **Many-to-Many**: Products ↔ Categories

---

## **Module 3: SQL Overview**

### **What is SQL?**

**SQL (Structured Query Language)** is a standardized programming language used to manage and manipulate relational databases. It is designed to interact with data stored in **Relational Database Management Systems (RDBMS)**, such as PostgreSQL, MySQL, SQL Server, and Oracle.

---

#### **1. Purpose of SQL**

SQL is used to:

1. **Query Data**:
    - Retrieve specific data from one or more tables.
    - Example: `SELECT * FROM Customers;`
2. **Insert Data**:
    - Add new records to a table.
    - Example: `INSERT INTO Orders (OrderID, CustomerID) VALUES (1, 101);`
3. **Update Data**:
    - Modify existing data in a table.
    - Example: `UPDATE Products SET Price = 20.99 WHERE ProductID = 5;`
4. **Delete Data**:
    - Remove records from a table.
    - Example: `DELETE FROM Customers WHERE CustomerID = 2;`
5. **Define Structure**:
    - Create, modify, or delete database structures like tables and indexes.
    - Example: `CREATE TABLE Orders (OrderID INT, OrderDate DATE);`
6. **Control Access**:
    - Grant and revoke permissions for database users.
    - Example: `GRANT SELECT ON Customers TO user_name;`

---

#### **2. Features of SQL**

1. **Declarative Language**:
    - SQL focuses on *what* you want to achieve rather than *how* to do it.
2. **Standardized**:
    - SQL is governed by standards (e.g., ANSI/ISO), making it portable across RDBMS systems with slight variations.
3. **Powerful**:
    - It supports complex operations like joins, aggregation, and nested queries.
4. **Extensible**:
    - Many RDBMS vendors provide extensions to standard SQL, such as procedural languages (PL/pgSQL in PostgreSQL).

---

#### **3. Components of SQL**

##### **3.1 SQL Sublanguages**

SQL can be divided into different sublanguages based on its functionality:

| **Sublanguage** | **Purpose** | **Examples** |
| --- | --- | --- |
| **DDL** | Data Definition Language: Defines database structure. | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`. |
| **DML** | Data Manipulation Language: Manipulates data. | `INSERT`, `UPDATE`, `DELETE`. |
| **DQL** | Data Query Language: Queries data. | `SELECT`. |
| **DCL** | Data Control Language: Manages permissions. | `GRANT`, `REVOKE`. |
| **TCL** | Transaction Control Language: Manages transactions. | `COMMIT`, `ROLLBACK`, `SAVEPOINT`. |

---

### **Overview of SQL Sublanguages**

SQL (Structured Query Language) can be divided into five distinct sublanguages, each serving a specific purpose in managing and interacting with relational databases. These sublanguages allow developers and administrators to define, manipulate, query, control, and manage transactions within a database.

---

#### **1. Data Definition Language (DDL)**

**Purpose**: Defines and modifies the structure of database objects like tables, schemas, indexes, and views.

### **Key Operations**:

| **Command** | **Description** | **Example** |
| --- | --- | --- |
| `CREATE` | Creates new database objects (e.g., tables, schemas). | `CREATE TABLE Users (UserID INT, Name TEXT);` |
| `ALTER` | Modifies the structure of an existing object. | `ALTER TABLE Users ADD Email TEXT;` |
| `DROP` | Deletes a database object. | `DROP TABLE Users;` |
| `TRUNCATE` | Removes all rows from a table without logging individual row deletions. | `TRUNCATE TABLE Users;` |

---

#### **2. Data Manipulation Language (DML)**

**Purpose**: Used to manipulate data stored in database tables.

#### **Key Operations**:

| **Command** | **Description** | **Example** |
| --- | --- | --- |
| `INSERT` | Adds new rows of data to a table. | `INSERT INTO Users (UserID, Name) VALUES (1, 'Alice');` |
| `UPDATE` | Modifies existing rows in a table. | `UPDATE Users SET Name = 'Bob' WHERE UserID = 1;` |
| `DELETE` | Removes rows from a table. | `DELETE FROM Users WHERE UserID = 1;` |

---

#### **3. Data Query Language (DQL)**

**Purpose**: Used to retrieve data from the database.

#### **Key Operation**:

| **Command** | **Description** | **Example** |
| --- | --- | --- |
| `SELECT` | Retrieves data based on specified criteria. | `SELECT Name, Email FROM Users WHERE UserID = 1;` |

---

#### **4. Data Control Language (DCL)**

**Purpose**: Manages access permissions and controls user privileges.

#### **Key Operations**:

| **Command** | **Description** | **Example** |
| --- | --- | --- |
| `GRANT` | Gives specific privileges to users or roles. | `GRANT SELECT ON Users TO admin;` |
| `REVOKE` | Removes specific privileges from users or roles. | `REVOKE SELECT ON Users FROM admin;` |

---

#### **5. Transaction Control Language (TCL)**

**Purpose**: Manages transactions to ensure data integrity and consistency.

#### **Key Operations**:

| **Command** | **Description** | **Example** |
| --- | --- | --- |
| `COMMIT` | Saves all changes made during the current transaction. | `COMMIT;` |
| `ROLLBACK` | Undoes changes made during the current transaction. | `ROLLBACK;` |
| `SAVEPOINT` | Sets a savepoint within a transaction to allow partial rollback. | `SAVEPOINT sp1;` |

---

#### **Summary of SQL Sublanguages**

| **Sublanguage** | **Purpose** | **Key Commands** |
| --- | --- | --- |
| **DDL** | Define and manage database structure. | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Manipulate data in tables. | `INSERT`, `UPDATE`, `DELETE` |
| **DQL** | Query and retrieve data. | `SELECT` |
| **DCL** | Manage permissions and security. | `GRANT`, `REVOKE` |
| **TCL** | Manage transactions for consistency. | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

#### **How the Sublanguages Work Together**

1. **DDL**: Defines the structure of the database.
    - Example: `CREATE TABLE Orders (OrderID INT, CustomerID INT);`
2. **DML**: Inserts or updates data within the defined structure.
    - Example: `INSERT INTO Orders VALUES (1, 101);`
3. **DQL**: Queries the inserted data.
    - Example: `SELECT * FROM Orders;`
4. **DCL**: Controls who can query or modify the data.
    - Example: `GRANT SELECT ON Orders TO user_name;`
5. **TCL**: Ensures that changes are either fully applied or fully undone.
    - Example: `BEGIN; UPDATE Orders SET CustomerID = 102 WHERE OrderID = 1; ROLLBACK;`

---

### **SQL Data Types in PostgreSQL**

SQL data types define the type of data that a column in a database table can store. PostgreSQL supports a wide variety of data types to handle different kinds of data.

---

#### **1. Categories of Data Types**

| **Category** | **Description** |
| --- | --- |
| **Numeric Types** | For numbers, including integers and decimals. |
| **Character Types** | For storing text or strings. |
| **Date/Time Types** | For storing dates, times, and timestamps. |
| **Boolean Type** | For storing `TRUE` or `FALSE`. |
| **UUID Type** | For universally unique identifiers. |
| **Array Types** | For storing arrays of a particular type. |
| **JSON/JSONB Types** | For storing JSON data in text or binary format. |
| **Geometric Types** | For geometric data like points, lines, and polygons. |
| **Binary Data Types** | For storing binary data, such as files or images. |
| **Other Types** | Includes `XML`, `ENUM`, `Range`, and more. |

---

#### **2. Commonly Used Data Types**

##### **2.1 Numeric Types**

| **Data Type** | **Description** | **Example Values** |
| --- | --- | --- |
| `SMALLINT` | A small integer (2 bytes). | `-32,768` to `32,767` |
| `INTEGER` / `INT` | A standard integer (4 bytes). | `-2,147,483,648` to `2,147,483,647` |
| `BIGINT` | A large integer (8 bytes). | `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807` |
| `DECIMAL(p, s)` | Exact numeric with precision and scale. | `123.45` |
| `NUMERIC(p, s)` | Same as `DECIMAL`. | `456.789` |
| `REAL` | Single-precision floating-point (4 bytes). | `3.14` |
| `DOUBLE PRECISION` | Double-precision floating-point (8 bytes). | `3.14159` |
| `SERIAL` | Auto-incrementing integer (4 bytes). | `1, 2, 3...` |
| `BIGSERIAL` | Auto-incrementing large integer (8 bytes). | `1, 2, 3...` |

---

##### **2.2 Character Types**

| **Data Type** | **Description** | **Example Values** |
| --- | --- | --- |
| `CHAR(n)` | Fixed-length character string (padded with spaces). | `'A'`, `'Hello '` |
| `VARCHAR(n)` | Variable-length character string with max length `n`. | `'Alice'`, `'Bob'` |
| `TEXT` | Variable-length character string (unlimited). | `'Lorem Ipsum...'` |

---

##### **2.3 Date/Time Types**

| **Data Type** | **Description** | **Example Values** |
| --- | --- | --- |
| `DATE` | Stores calendar dates. | `'2024-12-31'` |
| `TIME` | Stores time of day without time zone. | `'14:30:00'` |
| `TIMESTAMP` | Stores date and time without time zone. | `'2024-12-31 14:30:00'` |
| `TIMESTAMP WITH TIME ZONE` / `TIMESTAMPTZ` | Stores date and time with time zone information. | `'2024-12-31 14:30:00+01'` |
| `INTERVAL` | Stores a duration of time. | `'1 year 2 months'` |

---

##### **2.4 Boolean Type**

| **Data Type** | **Description** | **Example Values** |
| --- | --- | --- |
| `BOOLEAN` | Stores `TRUE`, `FALSE`, or `NULL`. | `TRUE`, `FALSE`, `NULL` |

---

##### **2.5 UUID Type**

| **Data Type** | **Description** | **Example Values** |
| --- | --- | --- |
| `UUID` | Universally unique identifier (128-bit value). | `'550e8400-e29b-41d4-a716-446655440000'` |

---

## **Module 4: Data Definition Language (DDL)**

### **Primary Key, Foreign Key, and Referential Integrity in PostgreSQL**

These concepts are fundamental in relational databases to establish and enforce relationships between tables and maintain data consistency.

---

#### **1. Primary Key**

##### **Definition**:

- A **primary key** is a column (or a combination of columns) in a table that uniquely identifies each row.
- Ensures no two rows in the table can have the same value for the primary key.
- It is automatically indexed for fast lookups.

##### **Characteristics**:

1. **Unique**:
    - No duplicate values are allowed.
2. **Non-NULL**:
    - Cannot contain `NULL` values.
3. **Single or Composite**:
    - Can consist of one column (single primary key) or multiple columns (composite primary key).

##### **Example**:

```sql
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,  -- Primary key ensures uniqueness
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(255) UNIQUE
);

```

- `CustomerID` is the primary key.
- PostgreSQL will enforce uniqueness and non-NULL constraints automatically.

---

#### **2. Foreign Key**

##### **Definition**:

- A **foreign key** is a column (or combination of columns) that establishes a link between data in two tables.
- It references the primary key in another table to enforce referential integrity.

##### **Characteristics**:

1. **Establishes Relationships**:
    - Defines the relationship between two tables (e.g., one-to-many or many-to-many).
2. **References a Primary Key**:
    - The foreign key must match a value in the referenced table's primary key or be `NULL`.

##### **Example**:

```sql
CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATE DEFAULT CURRENT_DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```

- `CustomerID` in the `Orders` table is a foreign key referencing `CustomerID` in the `Customers` table.
- This enforces the rule that every `CustomerID` in the `Orders` table must exist in the `Customers` table.

---

#### **3. Referential Integrity**

##### **Definition**:

- **Referential integrity** ensures that relationships between tables remain consistent.
- It prevents orphaned rows (i.e., rows that reference non-existent values).

##### **How It Works**:

1. **Insert**:
    - Prevents inserting a foreign key value that does not exist in the referenced table.
2. **Update**:
    - Ensures changes to the primary key in the referenced table propagate to the foreign key table or are restricted.
3. **Delete**:
    - Ensures deletions in the referenced table propagate to the foreign key table or are restricted.

---

### **PostgreSQL DDL Commands: CREATE, DROP, TRUNCATE, ALTER, DEFAULT, and CASCADE**

These **Data Definition Language (DDL)** commands define, modify, or remove the structure of database objects like tables, indexes, and schemas.

---

#### **1. CREATE**

The `CREATE` command is used to create new database objects such as tables, schemas, or indexes.

##### **Syntax**:

```sql
CREATE TABLE table_name (
    column_name data_type [constraint],
    ...
);

```

##### **Example**:

```sql
CREATE TABLE Employees (
    EmployeeID SERIAL PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Position VARCHAR(50),
    HireDate DATE DEFAULT CURRENT_DATE
);

```

- **Creates a table named `Employees`.**
- Includes `DEFAULT CURRENT_DATE` to set the default value for `HireDate`.

---

#### **2. DROP**

The `DROP` command removes a database object permanently. **Be cautious when using DROP, as it cannot be rolled back.**

##### **Syntax**:

```sql
DROP TABLE table_name [CASCADE];

```

##### **Example**:

```sql
DROP TABLE Employees;

```

- Removes the `Employees` table and its data.

##### **With CASCADE**:

```sql
DROP TABLE Employees CASCADE;

```

- Removes the `Employees` table **and** any dependent objects like foreign key constraints.

---

#### **3. TRUNCATE**

The `TRUNCATE` command removes all rows from a table but **does not remove the table structure**. It is faster than `DELETE` as it does not log individual row deletions.

##### **Syntax**:

```sql
TRUNCATE TABLE table_name;

```

##### **Example**:

```sql
TRUNCATE TABLE Employees;

```

- Removes all rows from the `Employees` table, resetting any auto-incremented columns.

---

#### **4. ALTER**

The `ALTER` command modifies the structure of an existing table, such as adding or removing columns, changing data types, or renaming the table.

##### **Syntax**:

```sql
ALTER TABLE table_name action;

```

##### **Actions**:

1. **Add a Column**:
    
    ```sql
    ALTER TABLE Employees ADD COLUMN Email VARCHAR(255);
    
    ```
    
2. **Drop a Column**:
    
    ```sql
    ALTER TABLE Employees DROP COLUMN Email;
    
    ```
    
3. **Modify a Column Type**:
    
    ```sql
    ALTER TABLE Employees ALTER COLUMN Name TYPE TEXT;
    
    ```
    
4. **Rename a Table**:
    
    ```sql
    ALTER TABLE Employees RENAME TO Staff;
    
    ```
    
5. **Rename a Column**:
    
    ```sql
    ALTER TABLE Employees RENAME COLUMN Name TO FullName;
    
    ```
    

---

#### **5. DEFAULT**

The `DEFAULT` constraint sets a default value for a column when no value is provided during an insert.

##### **Usage in CREATE TABLE**:

```sql
CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Price NUMERIC(10, 2) DEFAULT 0.00
);

```

- The `Price` column will default to `0.00` if no value is specified.

##### **Add DEFAULT with ALTER**:

```sql
ALTER TABLE Products ALTER COLUMN Price SET DEFAULT 10.00;

```

- Changes the default value of the `Price` column to `10.00`.

##### **Remove DEFAULT**:

```sql
ALTER TABLE Products ALTER COLUMN Price DROP DEFAULT;

```

---

#### **6. CASCADE**

The `CASCADE` option is used with commands like `DROP` and `TRUNCATE` to automatically apply the command to dependent objects.

##### **With DROP**:

```sql
DROP TABLE Orders CASCADE;

```

- Drops the `Orders` table and any foreign key constraints or dependent objects.

##### **With TRUNCATE**:

```sql
TRUNCATE TABLE Orders CASCADE;

```

- Removes all rows from the `Orders` table and its dependent tables.

##### **With Foreign Keys**:

```sql
CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) ON DELETE CASCADE
);

```

- If a `Customer` is deleted, all associated `Orders` are automatically deleted.

---

##### **Examples of Combined Usage**

##### **Scenario**: Managing a Simple Employee Database

1. **Create Table**:
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID SERIAL PRIMARY KEY,
        Name VARCHAR(100),
        Position VARCHAR(50),
        HireDate DATE DEFAULT CURRENT_DATE
    );
    
    ```
    
2. **Add a Column**:
    
    ```sql
    ALTER TABLE Employees ADD COLUMN Email VARCHAR(255);
    
    ```
    
3. **Set Default Value**:
    
    ```sql
    ALTER TABLE Employees ALTER COLUMN Position SET DEFAULT 'Trainee';
    
    ```
    
4. **Drop the Table**:
    
    ```sql
    DROP TABLE Employees CASCADE;
    
    ```
    

---

### **Comparison of DROP, TRUNCATE, and DELETE**

| **Command** | **Purpose** | **Removes Structure?** | **Rollback Possible?** | **Performance** |
| --- | --- | --- | --- | --- |
| `DROP` | Deletes the table and its data. | Yes | No | Fast |
| `TRUNCATE` | Deletes all rows in the table. | No | No | Fastest |
| `DELETE` | Deletes specific rows from the table. | No | Yes | Slower |

---

### **Constraints and Auto-Incrementing in PostgreSQL**

#### **1. Constraints**

**Constraints** enforce rules on table data to ensure accuracy, consistency, and integrity. PostgreSQL supports several types of constraints that can be applied to columns or tables.

---

##### **1.1 Types of Constraints**

| **Constraint** | **Description** |
| --- | --- |
| `NOT NULL` | Ensures a column cannot have `NULL` values. |
| `UNIQUE` | Ensures all values in a column or combination of columns are distinct. |
| `PRIMARY KEY` | Combines `NOT NULL` and `UNIQUE` to uniquely identify each row. |
| `FOREIGN KEY` | Establishes a relationship between tables. |
| `CHECK` | Ensures that all values in a column satisfy a specified condition. |
| `DEFAULT` | Sets a default value for a column when no value is provided during insertion. |

---

##### **1.2 Examples of Constraints**

1. **NOT NULL**:
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID SERIAL PRIMARY KEY,
        Name VARCHAR(100) NOT NULL
    );
    
    ```
    
2. **UNIQUE**:
    
    ```sql
    CREATE TABLE Customers (
        CustomerID SERIAL PRIMARY KEY,
        Email VARCHAR(255) UNIQUE
    );
    
    ```
    
3. **PRIMARY KEY**:
    
    ```sql
    CREATE TABLE Products (
        ProductID SERIAL PRIMARY KEY,
        ProductName VARCHAR(100) NOT NULL
    );
    
    ```
    
4. **FOREIGN KEY**:
    
    ```sql
    CREATE TABLE Orders (
        OrderID SERIAL PRIMARY KEY,
        CustomerID INT NOT NULL,
        FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
    );
    
    ```
    
5. **CHECK**:
    
    ```sql
    CREATE TABLE Accounts (
        AccountID SERIAL PRIMARY KEY,
        Balance NUMERIC(10, 2) CHECK (Balance >= 0)
    );
    
    ```
    
6. **DEFAULT**:
    
    ```sql
    CREATE TABLE Users (
        UserID SERIAL PRIMARY KEY,
        Role VARCHAR(50) DEFAULT 'User'
    );
    
    ```
    

---

#### **2. Auto-Incrementing Columns**

In PostgreSQL, **auto-incrementing** is achieved using the `SERIAL` or `BIGSERIAL` data types. These types automatically generate unique values for a column when a new row is inserted.

---

##### **2.1 Auto-Incrementing with SERIAL**

- `SERIAL` creates an auto-incrementing integer column.
- Automatically sets up a sequence to generate the values.

**Example**:

```sql
CREATE TABLE Employees (
    EmployeeID SERIAL PRIMARY KEY,
    Name VARCHAR(100) NOT NULL
);

```

- Inserts:
    
    ```sql
    INSERT INTO Employees (Name) VALUES ('Alice');
    INSERT INTO Employees (Name) VALUES ('Bob');
    
    ```
    
- Table after inserts:
    
    
    | EmployeeID | Name |
    | --- | --- |
    | 1 | Alice |
    | 2 | Bob |

---

##### **2.2 Auto-Incrementing with BIGSERIAL**

- `BIGSERIAL` is similar to `SERIAL` but uses a larger range of values (8 bytes).

**Example**:

```sql
CREATE TABLE Orders (
    OrderID BIGSERIAL PRIMARY KEY,
    OrderDate DATE DEFAULT CURRENT_DATE
);

```

---

## **Module 5: Data Manipulation Language (DML)**

### **DML Commands: INSERT, UPDATE, DELETE in PostgreSQL**

These **Data Manipulation Language (DML)** commands are used to add, modify, and remove data in a PostgreSQL table. They allow you to interact with the data stored in your database.

---

#### **1. INSERT**

The `INSERT` command is used to add new rows to a table.

##### **Basic Syntax**:

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);

```

##### **Examples**:

1. **Inserting a Single Row**:
    
    ```sql
    INSERT INTO Employees (Name, Position, HireDate)
    VALUES ('Alice', 'Developer', '2024-01-15');
    
    ```
    
2. **Inserting Multiple Rows**:
    
    ```sql
    INSERT INTO Employees (Name, Position, HireDate)
    VALUES
    ('Bob', 'Designer', '2024-02-01'),
    ('Charlie', 'Manager', '2024-03-01');
    
    ```
    
3. **Inserting Data Without Specifying Columns**:
    - Ensure values match the table’s column order:
    
    ```sql
    INSERT INTO Employees
    VALUES (1, 'Alice', 'Developer', '2024-01-15');
    
    ```
    
4. **Using DEFAULT Values**:
    
    ```sql
    INSERT INTO Employees (Name, Position)
    VALUES ('David', DEFAULT);  -- Defaults the HireDate column
    
    ```
    
5. **Copying Data from Another Table**:
    
    ```sql
    INSERT INTO Employees (Name, Position)
    SELECT Name, Role FROM Candidates WHERE Role IS NOT NULL;
    
    ```
    

---

#### **2. UPDATE**

The `UPDATE` command modifies existing rows in a table based on specified conditions.

##### **Basic Syntax**:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

```

##### **Examples**:

1. **Updating a Specific Row**:
    
    ```sql
    UPDATE Employees
    SET Position = 'Senior Developer', HireDate = '2023-12-01'
    WHERE Name = 'Alice';
    
    ```
    
2. **Updating Multiple Rows**:
    
    ```sql
    UPDATE Employees
    SET Position = 'Intern'
    WHERE HireDate > '2024-01-01';
    
    ```
    
3. **Updating All Rows**:
    - Be cautious when omitting the `WHERE` clause, as it updates all rows:
    
    ```sql
    UPDATE Employees
    SET Position = 'General Staff';
    
    ```
    
4. **Using Subqueries in UPDATE**:
    
    ```sql
    UPDATE Employees
    SET Position = (
        SELECT Role
        FROM Candidates
        WHERE Employees.Name = Candidates.Name
    );
    
    ```
    

---

#### **3. DELETE**

The `DELETE` command removes rows from a table based on specified conditions.

##### **Basic Syntax**:

```sql
DELETE FROM table_name
WHERE condition;

```

##### **Examples**:

1. **Deleting Specific Rows**:
    
    ```sql
    DELETE FROM Employees
    WHERE Name = 'Alice';
    
    ```
    
2. **Deleting Rows Based on a Condition**:
    
    ```sql
    DELETE FROM Employees
    WHERE HireDate < '2024-01-01';
    
    ```
    
3. **Deleting All Rows**:
    - Be cautious when omitting the `WHERE` clause, as it deletes all rows:
    
    ```sql
    DELETE FROM Employees;
    
    ```
    
4. **Using Subqueries in DELETE**:
    
    ```sql
    DELETE FROM Employees
    WHERE Name IN (
        SELECT Name
        FROM Candidates
        WHERE Role = 'Rejected'
    );
    
    ```
    

---

## **Module 6: Data Query Language (DQL)**

### **Queries, Aggregate Functions, WHERE, GROUP BY, and ORDER BY in PostgreSQL**

---

#### **1. Queries**

The `SELECT` statement is used to retrieve data from one or more tables in PostgreSQL.

##### **Basic Syntax**:

```sql
SELECT column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column1, column2, ...]
[HAVING condition]
[ORDER BY column1, column2, ...];

```

##### **Examples**:

1. **Select All Columns**:
    
    ```sql
    SELECT * FROM Employees;
    
    ```
    
2. **Select Specific Columns**:
    
    ```sql
    SELECT Name, Position FROM Employees;
    
    ```
    
3. **Select with a Condition**:
    
    ```sql
    SELECT * FROM Employees WHERE Position = 'Developer';
    
    ```
    

---

#### **2. Aggregate Functions**

Aggregate functions perform calculations on multiple rows and return a single value.

| **Function** | **Description** | **Example** |
| --- | --- | --- |
| `COUNT()` | Counts the number of rows. | `SELECT COUNT(*) FROM Employees;` |
| `SUM()` | Calculates the sum of a column. | `SELECT SUM(Salary) FROM Employees;` |
| `AVG()` | Calculates the average value. | `SELECT AVG(Salary) FROM Employees;` |
| `MIN()` | Finds the minimum value. | `SELECT MIN(Salary) FROM Employees;` |
| `MAX()` | Finds the maximum value. | `SELECT MAX(Salary) FROM Employees;` |

##### **Examples**:

1. **Count Rows**:
    
    ```sql
    SELECT COUNT(*) AS TotalEmployees FROM Employees;
    
    ```
    
2. **Sum of Salaries**:
    
    ```sql
    SELECT SUM(Salary) AS TotalSalary FROM Employees;
    
    ```
    
3. **Average Salary by Position**:
    
    ```sql
    SELECT Position, AVG(Salary) AS AverageSalary
    FROM Employees
    GROUP BY Position;
    
    ```
    

---

#### **3. WHERE Clause**

The `WHERE` clause filters rows based on specified conditions.

##### **Syntax**:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;

```

##### **Examples**:

1. **Filter by a Single Condition**:
    
    ```sql
    SELECT * FROM Employees WHERE Position = 'Manager';
    
    ```
    
2. **Filter by Multiple Conditions (AND/OR)**:
    
    ```sql
    SELECT * FROM Employees
    WHERE Position = 'Developer' AND Salary > 60000;
    
    ```
    
3. **Filter with IN**:
    
    ```sql
    SELECT * FROM Employees WHERE Position IN ('Manager', 'Developer');
    
    ```
    
4. **Filter with LIKE (Pattern Matching)**:
    
    ```sql
    SELECT * FROM Employees WHERE Name LIKE 'A%'; -- Names starting with 'A'
    
    ```
    
5. **Filter with Comparison Operators**:
    - `=`, `<`, `>`, `<=`, `>=`, `<>`
    
    ```sql
    SELECT * FROM Employees WHERE Salary > 50000;
    
    ```
    

---

#### **4. GROUP BY Clause**

The `GROUP BY` clause groups rows that have the same values in specified columns, often used with aggregate functions.

##### **Syntax**:

```sql
SELECT column1, column2, aggregate_function(column3)
FROM table_name
GROUP BY column1, column2;

```

##### **Examples**:

1. **Group Data by Position**:
    
    ```sql
    SELECT Position, COUNT(*) AS Count
    FROM Employees
    GROUP BY Position;
    
    ```
    
2. **Group Data with SUM**:
    
    ```sql
    SELECT DepartmentID, SUM(Salary) AS TotalSalary
    FROM Employees
    GROUP BY DepartmentID;
    
    ```
    
3. **Using GROUP BY with Multiple Columns**:
    
    ```sql
    SELECT DepartmentID, Position, AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY DepartmentID, Position;
    
    ```
    
4. **Filter Groups with HAVING**:
    - The `HAVING` clause filters groups (not rows like `WHERE`).
    
    ```sql
    SELECT Position, COUNT(*) AS Count
    FROM Employees
    GROUP BY Position
    HAVING COUNT(*) > 5;
    
    ```
    

---

#### **5. ORDER BY Clause**

The `ORDER BY` clause sorts the result set by one or more columns, either in ascending (`ASC`) or descending (`DESC`) order.

##### **Syntax**:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC | DESC];

```

##### **Examples**:

1. **Sort by a Single Column**:
    
    ```sql
    SELECT * FROM Employees ORDER BY Salary ASC;
    
    ```
    
2. **Sort by Multiple Columns**:
    
    ```sql
    SELECT * FROM Employees
    ORDER BY Position ASC, Salary DESC;
    
    ```
    
3. **Sort by an Aggregate Function**:
    
    ```sql
    SELECT Position, AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY Position
    ORDER BY AvgSalary DESC;
    
    ```
    

---

## **Module 7: Joins**

### **Joins in PostgreSQL**

A **Join** combines rows from two or more tables based on a related column. It allows you to retrieve data spread across multiple tables by establishing relationships.

---

### **1. Types of Joins**

| **Type** | **Description** |
| --- | --- |
| **Cross Join** | Combines every row from one table with every row from another table (Cartesian product). |
| **Equi Join** | A join based on equality between columns (a subset of inner joins). |
| **Theta Join** | A join using a condition that is not equality (e.g., `>`, `<`). |
| **Inner Join** | Returns rows where there is a match in both tables. |
| **Left Join** | Returns all rows from the left table and matching rows from the right table. |
| **Right Join** | Returns all rows from the right table and matching rows from the left table. |
| **Outer Join** | Combines left, right, and unmatched rows from both tables. |
| **Aliases** | Temporary names assigned to tables or columns to simplify queries. |
| **Subquery** | A query nested within another query, used to filter or derive data. |

---

#### **2. Cross Join**

##### **Definition**:

- Produces a Cartesian product, pairing each row in the first table with every row in the second table.
- Rarely used directly due to the large output size.

##### **Syntax**:

```sql
SELECT *
FROM table1
CROSS JOIN table2;

```

##### **Example**:

```sql
SELECT *
FROM Employees
CROSS JOIN Departments;

```

- If `Employees` has 3 rows and `Departments` has 2 rows, the result will have  rows.
    
    3×2=63 \times 2 = 6
    

---

#### **3. Equi and Theta Joins**

##### **Equi Join**:

- Combines rows where specified columns in both tables are equal.
- A subset of inner joins.

##### **Syntax**:

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.column = table2.column;

```

##### **Example**:

```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
INNER JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;

```

##### **Theta Join**:

- Uses a condition other than equality (e.g., `<`, `>`, `!=`).

##### **Example**:

```sql
SELECT *
FROM Products p
JOIN Orders o
ON p.Price > o.DiscountedPrice;

```

---

#### **4. Inner Join**

##### **Definition**:

- Returns rows where there is a match in both tables.

##### **Syntax**:

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.column = table2.column;

```

##### **Example**:

```sql
SELECT Employees.Name, Orders.OrderID
FROM Employees
INNER JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;

```

- Only includes employees who have placed orders.

---

#### **5. Left Join**

##### **Definition**:

- Returns all rows from the left table and matching rows from the right table. If no match, the result contains `NULL` for the right table's columns.

##### **Syntax**:

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;

```

##### **Example**:

```sql
SELECT Employees.Name, Orders.OrderID
FROM Employees
LEFT JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;

```

- Includes all employees, even those who have not placed orders (with `NULL` in the `OrderID` column).

---

#### **6. Right Join**

##### **Definition**:

- Returns all rows from the right table and matching rows from the left table. If no match, the result contains `NULL` for the left table's columns.

##### **Syntax**:

```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;

```

##### **Example**:

```sql
SELECT Employees.Name, Orders.OrderID
FROM Employees
RIGHT JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;

```

- Includes all orders, even those with no corresponding employee (with `NULL` in the `Name` column).

---

#### **7. Outer Join**

##### **Definition**:

- Combines results of left join, right join, and unmatched rows from both tables.

##### **Syntax**:

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;

```

##### **Example**:

```sql
SELECT Employees.Name, Orders.OrderID
FROM Employees
FULL OUTER JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;

```

- Includes all employees and all orders, with `NULL` for missing matches on either side.

---

#### **8. Aliases**

##### **Definition**:

- Temporary names for tables or columns to simplify queries.

##### **Syntax**:

```sql
SELECT column_name AS alias_name
FROM table_name AS alias_name;

```

##### **Examples**:

1. **Column Alias**:
    
    ```sql
    SELECT Name AS EmployeeName, Salary AS MonthlySalary
    FROM Employees;
    
    ```
    
2. **Table Alias**:
    
    ```sql
    SELECT e.Name, d.DepartmentName
    FROM Employees AS e
    JOIN Departments AS d
    ON e.DepartmentID = d.DepartmentID;
    
    ```
    

---

#### **9. Subqueries**

##### **Definition**:

- A query nested within another query, used to filter or derive data.

##### **Types of Subqueries**:

1. **Scalar Subquery**: Returns a single value.
2. **Row Subquery**: Returns a single row.
3. **Table Subquery**: Returns multiple rows/columns.

##### **Syntax**:

```sql
SELECT column1, column2
FROM table1
WHERE column1 = (SELECT column FROM table2 WHERE condition);

```

##### **Examples**:

1. **Scalar Subquery**:
    
    ```sql
    SELECT Name
    FROM Employees
    WHERE Salary > (SELECT AVG(Salary) FROM Employees);
    
    ```
    
    - Finds employees earning above the average salary.
2. **Row Subquery**:
    
    ```sql
    SELECT Name
    FROM Employees
    WHERE (DepartmentID, Salary) = (SELECT DepartmentID, MAX(Salary) FROM Employees);
    
    ```
    
    - Finds the highest-paid employee in each department.
3. **Table Subquery**:
    
    ```sql
    SELECT *
    FROM Employees
    WHERE EmployeeID IN (SELECT EmployeeID FROM Orders WHERE OrderDate > '2024-01-01');
    
    ```
    
    - Finds employees who placed orders after January 1, 2024.

---

## **Module 8: Transactions**

### **Transactions in PostgreSQL**

A **transaction** in PostgreSQL is a sequence of one or more SQL statements that are executed as a single unit of work. Transactions ensure the database remains consistent and reliable even in the face of errors or failures.

---

##### **1. What is a Transaction?**

A transaction is a logical unit of database operations that:

1. Groups multiple statements together.
2. Executes them as a single operation.
3. Ensures either all operations succeed, or none are applied (atomicity).

##### **Key Commands**:

- **BEGIN**: Starts a transaction.
- **COMMIT**: Saves changes made during the transaction.
- **ROLLBACK**: Undoes changes made during the transaction.

---

#### **2. Transaction Commands**

##### **2.1 BEGIN**

Starts a transaction block.

**Syntax**:

```sql
BEGIN;

```

**Example**:

```sql
BEGIN;
INSERT INTO Accounts (AccountID, Balance) VALUES (101, 5000);
UPDATE Accounts SET Balance = Balance - 1000 WHERE AccountID = 101;

```

---

##### **2.2 COMMIT**

Saves all changes made in the current transaction and makes them permanent.

**Syntax**:

```sql
COMMIT;

```

**Example**:

```sql
BEGIN;
UPDATE Accounts SET Balance = Balance - 1000 WHERE AccountID = 101;
INSERT INTO Transactions (AccountID, Amount, Type) VALUES (101, 1000, 'Debit');
COMMIT;

```

---

##### **2.3 ROLLBACK**

Cancels all changes made during the current transaction, restoring the database to its previous state.

**Syntax**:

```sql
ROLLBACK;

```

**Example**:

```sql
BEGIN;
UPDATE Accounts SET Balance = Balance - 1000 WHERE AccountID = 101;
-- Some error occurs
ROLLBACK; -- Reverts the changes

```

---

##### **2.4 SAVEPOINT**

Creates a savepoint within a transaction to allow partial rollbacks.

**Syntax**:

```sql
SAVEPOINT savepoint_name;
ROLLBACK TO savepoint_name;

```

**Example**:

```sql
BEGIN;
INSERT INTO Orders (OrderID, Amount) VALUES (1, 500);
SAVEPOINT sp1;
INSERT INTO Orders (OrderID, Amount) VALUES (2, 1000);
ROLLBACK TO sp1; -- Reverts the second insert only
COMMIT;

```

---

#### **3. Transaction Properties (ACID)**

Transactions must adhere to the **ACID** properties to ensure data consistency and reliability.

| **Property** | **Description** |
| --- | --- |
| **Atomicity** | Ensures all operations in a transaction are completed or none at all. |
| **Consistency** | Ensures the database remains in a valid state before and after the transaction. |
| **Isolation** | Ensures transactions do not interfere with each other. |
| **Durability** | Ensures changes made by a committed transaction are permanent. |

---

#### **4. Isolation Levels**

**Isolation levels** define how much a transaction is isolated from other transactions. PostgreSQL supports four isolation levels.

| **Isolation Level** | **Description** | **Example Use Case** |
| --- | --- | --- |
| **Read Uncommitted** | Transactions can read uncommitted changes made by others. | Rarely used due to potential dirty reads. |
| **Read Committed (Default)** | A transaction only sees changes committed before it starts. | Standard for many applications. |
| **Repeatable Read** | Ensures consistent reads; data won't change within the transaction, but allows phantom reads. | Complex reporting or batch processes. |
| **Serializable** | Provides full isolation; transactions appear as if they run sequentially. | Critical for financial systems or consistency. |

##### **Set Isolation Level**:

```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;

```

---

#### **5. Examples of Isolation Levels**

##### **5.1 Dirty Read**:

Occurs at `Read Uncommitted` level when a transaction reads uncommitted changes from another transaction.

**Example**:

- Transaction 1: Updates a row but doesn’t commit.
- Transaction 2: Reads the updated row before Transaction 1 commits.

---

##### **5.2 Non-Repeatable Read**:

Occurs at `Read Committed` level when data read by a transaction is modified by another transaction before the first one completes.

**Example**:

- Transaction 1: Reads a row.
- Transaction 2: Updates the same row and commits.
- Transaction 1 reads the row again and sees the updated value.

---

##### **5.3 Phantom Read**:

Occurs at `Repeatable Read` level when new rows added by another transaction appear in subsequent reads of the same query.

**Example**:

- Transaction 1: Queries rows with a condition.
- Transaction 2: Inserts new rows matching the condition and commits.
- Transaction 1 re-executes the query and sees the new rows.

---

#### **6. Practical Examples**

##### **Basic Transaction**:

```sql
BEGIN;
INSERT INTO Accounts (AccountID, Balance) VALUES (1, 1000);
UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
COMMIT;

```

##### **Transaction with Rollback**:

```sql
BEGIN;
INSERT INTO Orders (OrderID, CustomerID, Total) VALUES (1, 101, 500);
UPDATE Customers SET Balance = Balance - 500 WHERE CustomerID = 101;
-- Simulate an error
ROLLBACK;

```

##### **Savepoints for Partial Rollback**:

```sql
BEGIN;
INSERT INTO Products (ProductID, Name, Price) VALUES (1, 'Product A', 100);
SAVEPOINT sp1;
INSERT INTO Products (ProductID, Name, Price) VALUES (2, 'Product B', 200);
ROLLBACK TO sp1; -- Reverts the second insert
COMMIT;

```

---

#### **7. Summary**

| **Feature** | **Description** |
| --- | --- |
| **BEGIN** | Starts a transaction. |
| **COMMIT** | Saves all changes made during the transaction. |
| **ROLLBACK** | Reverts all changes made during the transaction. |
| **SAVEPOINT** | Creates a checkpoint for partial rollbacks within a transaction. |
| **Isolation Levels** | Controls how transactions interact with one another. |
| **ACID Properties** | Ensures transactions are atomic, consistent, isolated, and durable. |

---

## **Module 9: Advanced SQL**

### **Advanced SQL Concepts in PostgreSQL**

---

#### **1. Indexes**

##### **Definition**:

An **index** is a database object that improves the performance of data retrieval operations by allowing quick access to rows in a table.

### **Types of Indexes**:

1. **B-Tree Index** (Default):
    - Suitable for equality and range queries.
2. **Hash Index**:
    - Useful for equality comparisons.
3. **GIN/GIN Indexes**:
    - Used for full-text search and JSONB operations.
4. **Partial Index**:
    - Applied only to rows that meet a condition.
5. **Unique Index**:
    - Ensures all values in a column are unique.

##### **Syntax**:

```sql
CREATE INDEX index_name ON table_name (column_name);

```

##### **Examples**:

1. **Creating a Simple Index**:
    
    ```sql
    CREATE INDEX idx_name ON Employees (Name);
    
    ```
    
2. **Creating a Unique Index**:
    
    ```sql
    CREATE UNIQUE INDEX idx_email ON Users (Email);
    
    ```
    
3. **Partial Index**:
    
    ```sql
    CREATE INDEX idx_active_users ON Users (LastLogin) WHERE Active = TRUE;
    
    ```
    
4. **Dropping an Index**:
    
    ```sql
    DROP INDEX idx_name;
    
    ```
    

---

#### **2. Scalar Functions**

##### **Definition**:

A **scalar function** operates on a single value and returns a single value. PostgreSQL has a wide range of built-in scalar functions.

##### **Examples**:

1. **String Functions**:
    
    ```sql
    SELECT UPPER('hello'); -- Returns 'HELLO'
    SELECT LENGTH('hello'); -- Returns 5
    
    ```
    
2. **Mathematical Functions**:
    
    ```sql
    SELECT ROUND(123.456, 2); -- Returns 123.46
    SELECT ABS(-10); -- Returns 10
    
    ```
    
3. **Date/Time Functions**:
    
    ```sql
    SELECT CURRENT_DATE; -- Returns today's date
    SELECT AGE(TIMESTAMP '2024-01-01'); -- Returns the age from the given date
    
    ```
    
4. **Casting Functions**:
    
    ```sql
    SELECT CAST(123 AS TEXT); -- Converts integer to text
    
    ```
    

---

#### **3. Views**

##### **Definition**:

A **view** is a virtual table based on the result of a query. Views are used to simplify complex queries, secure sensitive data, and improve code reusability.

##### **Syntax**:

```sql
CREATE VIEW view_name AS
SELECT columns
FROM table_name
WHERE condition;

```

##### **Examples**:

1. **Creating a View**:
    
    ```sql
    CREATE VIEW ActiveEmployees AS
    SELECT Name, Position
    FROM Employees
    WHERE Status = 'Active';
    
    ```
    
2. **Using a View**:
    
    ```sql
    SELECT * FROM ActiveEmployees;
    
    ```
    
3. **Updating a View**:
    
    ```sql
    CREATE OR REPLACE VIEW ActiveEmployees AS
    SELECT Name, Position, Department
    FROM Employees
    WHERE Status = 'Active';
    
    ```
    
4. **Dropping a View**:
    
    ```sql
    DROP VIEW ActiveEmployees;
    
    ```
    

---

#### **4. Sequences**

##### **Definition**:

A **sequence** is a database object that generates unique numbers, typically used for primary key values.

##### **Syntax**:

```sql
CREATE SEQUENCE sequence_name START WITH start_value INCREMENT BY increment_value;

```

##### **Examples**:

1. **Creating a Sequence**:
    
    ```sql
    CREATE SEQUENCE seq_order_id START WITH 1 INCREMENT BY 1;
    
    ```
    
2. **Using a Sequence**:
    
    ```sql
    INSERT INTO Orders (OrderID, CustomerID)
    VALUES (NEXTVAL('seq_order_id'), 101);
    
    ```
    
3. **Viewing Sequence Information**:
    
    ```sql
    SELECT LAST_VALUE FROM seq_order_id;
    
    ```
    
4. **Resetting a Sequence**:
    
    ```sql
    ALTER SEQUENCE seq_order_id RESTART WITH 1;
    
    ```
    

---

#### **5. Trigger**

##### **Definition**:

A **trigger** is a database callback function that automatically executes in response to a specific event (e.g., `INSERT`, `UPDATE`, `DELETE`) on a table.

##### **Syntax**:

```sql
CREATE TRIGGER trigger_name
AFTER INSERT OR UPDATE OR DELETE
ON table_name
FOR EACH ROW
EXECUTE FUNCTION function_name();

```

##### **Examples**:

1. **Creating a Trigger**:
    
    ```sql
    CREATE OR REPLACE FUNCTION log_changes()
    RETURNS TRIGGER AS $$
    BEGIN
        INSERT INTO Logs (TableName, Action, Timestamp)
        VALUES (TG_TABLE_NAME, TG_OP, CURRENT_TIMESTAMP);
        RETURN NEW;
    END;
    $$ LANGUAGE plpgsql;
    
    CREATE TRIGGER after_employee_change
    AFTER INSERT OR UPDATE OR DELETE
    ON Employees
    FOR EACH ROW
    EXECUTE FUNCTION log_changes();
    
    ```
    
2. **Dropping a Trigger**:
    
    ```sql
    DROP TRIGGER after_employee_change ON Employees;
    
    ```
    

---

#### **6. What is a Stored Procedure?**

##### **Definition**:

A **stored procedure** is a precompiled collection of SQL statements and control logic stored in the database. It can be executed with a single call.

##### **Syntax**:

```sql
CREATE PROCEDURE procedure_name (parameters)
LANGUAGE plpgsql
AS $$
BEGIN
    -- SQL statements
END;
$$;

```

##### **Example**:

```sql
CREATE PROCEDURE add_employee(name VARCHAR, position VARCHAR, salary NUMERIC)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO Employees (Name, Position, Salary)
    VALUES (name, position, salary);
END;
$$;

CALL add_employee('Alice', 'Manager', 60000);

```

---

#### **7. What is a User-Defined Function (UDF)?**

##### **Definition**:

A **user-defined function** (UDF) is a custom function created by the user to perform a specific task. Unlike procedures, functions return a value.

##### **Syntax**:

```sql
CREATE FUNCTION function_name (parameters)
RETURNS return_type
LANGUAGE plpgsql
AS $$
BEGIN
    -- SQL statements
    RETURN value;
END;
$$;

```

##### **Examples**:

1. **Creating a Function**:
    
    ```sql
    CREATE FUNCTION calculate_bonus(salary NUMERIC)
    RETURNS NUMERIC
    LANGUAGE plpgsql
    AS $$
    BEGIN
        RETURN salary * 0.10;
    END;
    $$;
    
    ```
    
2. **Calling a Function**:
    
    ```sql
    SELECT calculate_bonus(50000); -- Returns 5000
    
    ```
    
3. **Dropping a Function**:
    
    ```sql
    DROP FUNCTION calculate_bonus;
    
    ```
    

---

##### **Comparison: Stored Procedure vs. User-Defined Function**

| **Aspect** | **Stored Procedure** | **User-Defined Function** |
| --- | --- | --- |
| **Returns a Value** | No (but can use `OUT` parameters). | Yes, always returns a value. |
| **Usage in Queries** | Cannot be used in SQL queries. | Can be used in `SELECT`, `WHERE`, etc. |
| **Call Syntax** | `CALL procedure_name();` | `SELECT function_name();` |
| **Side Effects** | Can modify database state. | Typically used for computations, not state changes. |

---