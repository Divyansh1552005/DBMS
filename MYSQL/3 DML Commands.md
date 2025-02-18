
## **Data Manipulation Language (DML) Commands in MySQL**

DML commands in MySQL are used to manipulate data within tables. Unlike DDL commands, DML operations can be rolled back using transaction control commands.

---

## **1. INSERT Command**

The `INSERT` command is used to add new records to a table.

### **Syntax:**

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

```sql
INSERT INTO table_name (column1, column2, ...) VALUES
(value1_1, value1_2, ...),
(value2_1, value2_2, ...),
(value3_1, value3_2, ...);
```
### **Example:**

```sql
INSERT INTO Employees (ID, Name, Age, Salary)
VALUES (1, 'John Doe', 30, 50000);
```

This inserts a new record into the `Employees` table.

---

## **2. SELECT Command**

The `SELECT` command is used to retrieve data from a table.

### **Syntax:**

```sql
SELECT column1, column2 FROM table_name;
```

### **Example:**

```sql
SELECT Name, Salary FROM Employees;
```

This retrieves the `Name` and `Salary` columns from the `Employees` table.

#### **Selecting All Columns:**

```sql
SELECT * FROM Employees;
```

This selects all columns from the `Employees` table.

#### **Using WHERE Clause:**

```sql
SELECT * FROM Employees WHERE Age > 25;
```

This retrieves employees older than 25.

---

## **3. UPDATE Command**

The `UPDATE` command is used to modify existing records in a table.

### **Syntax:**

```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```

### **Example:**

```sql
UPDATE Employees SET Salary = 60000 WHERE ID = 1;
```

This updates the `Salary` of the employee with `ID = 1` to `60000`.

---

## **4. DELETE Command**

The `DELETE` command is used to remove records from a table.

### **Syntax:**

```sql
DELETE FROM table_name WHERE condition;
```

### **Example:**

```sql
DELETE FROM Employees WHERE Age < 25;
```

This deletes all employees younger than 25.

#### **Deleting All Records (Without Dropping the Table):**

```sql
DELETE FROM Employees;
```

This removes all records from the `Employees` table but keeps the table structure intact.

---

## **5. TRUNCATE vs DELETE**

- `DELETE`: Removes records but allows rollback if used within a transaction.
- `TRUNCATE`: Removes all records but is not rollbackable, resetting auto-increment counters.

### **Example:**

```sql
TRUNCATE TABLE Employees;
```

This deletes all data from the `Employees` table but retains the table structure.

---

## **Transaction Control with DML**

DML commands can be controlled using transactions.

### **Example:**

```sql
START TRANSACTION;
UPDATE Employees SET Salary = 70000 WHERE ID = 1;
ROLLBACK;  -- Reverts the update
COMMIT;    -- Saves the update permanently
```

This ensures changes can be reverted (`ROLLBACK`) or made permanent (`COMMIT`).

---

DML commands help in managing and modifying data efficiently in MySQL databases.

![[Pasted image 20250216124715.png]]


![[Pasted image 20250216124753.png]]


Note - 
Delete :- 
i. Tuples are deleted one by one 
ii. We can use WHERE clause to add conditions 
iii. Slow 
iv. Log is generated so we can ROLLBACK to some previous state 
Truncate :- 
i. All the Tuples are deleted at one go 
ii. Use of WHERE clause is not allowed 
iii. Fast 
iv. No Log is generated

[[4 Others imp things for SELECT Command]]
