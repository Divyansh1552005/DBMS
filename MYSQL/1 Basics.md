SQL (Structured Query Language) is used to interact with relational databases. It allows users to **create**, **retrieve**, **update**, and **delete** data.SQL (Structured Query Language) is a **declarative language** used for managing relational databases, meaning users specify **what** they want to retrieve or modify rather than detailing **how** to do it.  Also it is not case-sensitive.

SQL commands are categorized into five main types based on their functionalities:

1. **DDL (Data Definition Language)** – Defines database structure.
2. **DML (Data Manipulation Language)** – Modifies data in tables.
3. **DQL (Data Query Language)** – Retrieves data.
4. **DCL (Data Control Language)** – Manages permissions.
5. **TCL (Transaction Control Language)** – Controls transactions.


## History of SQL

It was developed in the 1970s at IBM by **Donald D. Chamberlin** and **Raymond F. Boyce**, based on **Dr. Edgar F. Codd’s** relational model. Originally called **SEQUEL**, it was later renamed SQL due to trademark issues. SQL became the standard for database management when **Oracle** released the first commercial SQL-based RDBMS in 1979. Over time, it evolved into an **ANSI and ISO standard**, making it the most widely used database language globally.


## Categorisation in SQL
SQL (Structured Query Language) commands are categorized into different types based on their functionality.

1. **Data Definition Language (DDL)**: These commands define and manage the structure of database objects like tables and schemas. Examples include `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, and `RENAME`.
    
2. **Data Manipulation Language (DML)**: These commands handle data operations such as retrieval, insertion, modification, and deletion. Examples include `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.
    
3. **Data Control Language (DCL)**: These commands control access and permissions to the database. The main commands are `GRANT` and `REVOKE`.
    
4. **Transaction Control Language (TCL)**: These commands manage database transactions to ensure consistency and integrity. Examples include `COMMIT`, `ROLLBACK`, and `SAVEPOINT`.
    
5. **Constraints**: Constraints define rules to ensure the accuracy and integrity of data in a table. Common constraints include `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, `UNIQUE`, `DEFAULT`, and `NOT NULL`.

Note- **DQL (Data Query Language)** is a subset of SQL that focuses on retrieving data from the database. The primary command in DQL is:

- **`SELECT`**: Used to fetch data from one or more tables based on specified conditions.

DQL is sometimes considered part of **DML**, but it's often categorized separately because it only deals with querying data, not modifying it.


[[2 DDL Commands + Database commands]]

