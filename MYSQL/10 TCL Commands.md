
## 📘 What is a Transaction?

A **transaction** is a sequence of one or more SQL operations executed as a single unit of work. A transaction must be either **fully completed** or **fully aborted** — never left halfway.

### 🔄 ACID Properties

Transactions follow ACID properties:

- **A**tomicity
- **C**onsistency
- **I**solation
- **D**urability

---

## 🧪 TCL - Transaction Control Language

TCL commands are used to manage transactions in SQL.

### 🔹 1. `START TRANSACTION` / `BEGIN`

Used to begin a new transaction.

```sql
START TRANSACTION;
-- or
BEGIN;
```

#### Example:

```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 500 WHERE acc_id = 101;
UPDATE accounts SET balance = balance + 500 WHERE acc_id = 102;
```

---

### 🔹 2. `COMMIT`

Used to **save** all changes made in the current transaction permanently to the database.

#### Example:

```sql
START TRANSACTION;
UPDATE products SET stock = stock - 2 WHERE product_id = 1;
COMMIT;
```

➡️ Inventory update is now **permanent**.

---

### 🔹 3. `ROLLBACK`

Used to **undo** changes made in the current transaction.

#### Example:

```sql
START TRANSACTION;
UPDATE orders SET status = 'Shipped' WHERE order_id = 5001;
ROLLBACK;
```

➡️ `status` change is **cancelled**.

---

### 🔹 4. `SAVEPOINT`

Creates a named **savepoint** in a transaction to which you can later roll back.

#### Example:

```sql
START TRANSACTION;
UPDATE students SET grade = 'B' WHERE id = 1;
SAVEPOINT sp1;
UPDATE students SET grade = 'A' WHERE id = 2;
ROLLBACK TO sp1;
COMMIT;
```

➡️ Only the first update remains.

---

### 🔹 5. `ROLLBACK TO SAVEPOINT`

Rolls back the transaction to a previously defined savepoint.

#### Example:

```sql
START TRANSACTION;
INSERT INTO logs VALUES ('Step 1');
SAVEPOINT step1;
INSERT INTO logs VALUES ('Step 2');
SAVEPOINT step2;
ROLLBACK TO step1;
COMMIT;
```

➡️ Only `Step 1` is committed.

---

## 🧑‍🔬 Real Table Example

Suppose we have a table:

```sql
CREATE TABLE bank (
    acc_no INT PRIMARY KEY,
    name VARCHAR(50),
    balance INT
);

INSERT INTO bank VALUES (1, 'Alice', 1000), (2, 'Bob', 1000);
```

### 🎯 Transaction Example with all TCL commands:

```sql
START TRANSACTION;
-- Alice sends 200 to Bob
UPDATE bank SET balance = balance - 200 WHERE acc_no = 1;
SAVEPOINT after_alice;
UPDATE bank SET balance = balance + 200 WHERE acc_no = 2;
-- Something goes wrong, rollback only Bob's update
ROLLBACK TO after_alice;
-- Fix the issue and commit
UPDATE bank SET balance = balance + 200 WHERE acc_no = 2;
COMMIT;
```

---

## 🧾 Summary Table

|Command|Description|
|---|---|
|`START TRANSACTION`|Begins a new transaction|
|`COMMIT`|Saves changes permanently|
|`ROLLBACK`|Undoes all changes in current transaction|
|`SAVEPOINT`|Sets a rollback point|
|`ROLLBACK TO`|Reverts to a specific savepoint|

---

## 📌 Notes

- Not all databases support all TCL commands the same way.
    
- Use transactions for **banking**, **inventory**, **critical updates**.
    

> Always test your transactions before committing in a production system.



