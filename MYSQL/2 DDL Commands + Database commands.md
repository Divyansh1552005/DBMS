
# **MySQL Data Types**

MySQL supports various data types categorized as follows:

## **1. Numeric Data Types:**

- `INT` (Integer)
- `BIGINT` (Large integer)
- `DECIMAL(p,s)` (Fixed-point number)
- `FLOAT` (Floating-point number)
- `DOUBLE` (Double-precision floating-point number)

- **`p` (precision)** = total number of **digits** that can be stored (both left and right of the decimal point).
- **`s` (scale)** = number of **digits after the decimal point**.
## **2. String Data Types:**

- `CHAR(n)` (Fixed-length string)
- `VARCHAR(n)` (Variable-length string)
- `TEXT` (Large text string)

## **3. Date & Time Data Types:**

- `DATE` (YYYY-MM-DD)
- `DATETIME` (YYYY-MM-DD HH:MI:SS)
- `TIMESTAMP` (Auto-updating timestamp)

## **4. Boolean Data Type:**

- `BOOLEAN` (Stores TRUE/FALSE as 1/0)

---

# **Database Specific Commands**

## **1. CREATE DATABASE**

### **Syntax:**

```sql
CREATE DATABASE database_name;
```

### **Example:**

```sql
CREATE DATABASE CompanyDB;
```

## **2. SHOW DATABASES**

### **Syntax:**

```sql
SHOW DATABASES;
```

## **3. DROP DATABASE**

### **Syntax:**

```sql
DROP DATABASE database_name;
```

### **Example:**

```sql
DROP DATABASE CompanyDB;
```

## **4. USE DATABASE**

### **Syntax:**

```sql
USE database_name;
```

### **Example:**

```sql
USE CompanyDB;
```

## **5. SHOW TABLES**

### **Syntax:**

```sql
SHOW TABLES;
```

---

# **Data Definition Language (DDL) Commands in MySQL**

DDL commands in MySQL are used to define, modify, and delete database objects like tables, indexes, and schemas. These commands directly affect the database structure.

## **1. CREATE TABLE**

### **Syntax:**

```sql
CREATE TABLE table_name (
    column1 datatype CONSTRAINT,
    column2 datatype CONSTRAINT,
    ...
);
```

### **Example:**

```sql
CREATE TABLE Employees (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(50) NOT NULL,
    Age INT CHECK (Age > 18),
    Salary DECIMAL(10,2) DEFAULT 50000
);
```

## **2. DESCRIBE TABLE**

### **Syntax:**

```sql
DESC table_name;
```

### **Example:**

```sql
DESC Employees;
```

## **3. ALTER TABLE**

### **Adding a new column:**

#### **Syntax:**

```sql
ALTER TABLE table_name ADD column_name datatype;
```

#### **Example:**

```sql
ALTER TABLE Employees ADD Department VARCHAR(50);
```

### **Modifying a column datatype:**

#### **Syntax:**

```sql
ALTER TABLE table_name MODIFY column_name new_datatype;
```

#### **Example:**

```sql
ALTER TABLE Employees MODIFY Salary FLOAT;
```

### **Dropping a column:**

#### **Syntax:**

```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

#### **Example:**

```sql
ALTER TABLE Employees DROP COLUMN Age;
```

### **Renaming a column:**

#### **Syntax:**

```sql
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
```

#### **Example:**

```sql
ALTER TABLE Employees RENAME COLUMN Name TO FullName;
```

### **Renaming a table:**

#### **Syntax:**

```sql
RENAME TABLE old_table_name TO new_table_name;
```

#### **Example:**

```sql
RENAME TABLE Employees TO Staff;
```

### **Adding a constraint:**

#### **Syntax:**

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name constraint_type (column_name);
```

#### **Example:**

```sql
ALTER TABLE Employees ADD CONSTRAINT chk_salary CHECK (Salary > 30000);
```

### **Dropping a constraint:**

#### **Syntax:**

```sql
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

#### **Example:**

```sql
ALTER TABLE Employees DROP CONSTRAINT chk_salary;
```

## **4. DROP TABLE**

### **Syntax:**

```sql
DROP TABLE table_name;
```

### **Example:**

```sql
DROP TABLE Employees;
```

## **5. TRUNCATE TABLE**

### **Syntax:**

```sql
TRUNCATE TABLE table_name;
```

### **Example:**

```sql
TRUNCATE TABLE Employees;
```

### **Difference between DROP and TRUNCATE:**

- `DROP TABLE` removes both data and table structure.
- `TRUNCATE TABLE` removes only the data but keeps the table structure.

## **Constraints in MySQL**

Constraints are rules applied to table columns to ensure data integrity and consistency.

### **Types of Constraints:**

- `PRIMARY KEY`: Ensures uniqueness + not null value in a column.
- `FOREIGN KEY`: Establishes a relationship between two tables.
- `CHECK`: Ensures a column value meets a condition.
- `UNIQUE`: Ensures all values in a column are distinct.
- `DEFAULT`: Assigns a default value if none is provided.
- `NOT NULL`: Ensures a column cannot have NULL values.

DDL commands **do not require COMMIT** because they are auto-committed, meaning changes are permanent immediately.

[[3 DML Commands]]