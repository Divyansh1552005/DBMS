# **Keys in SQL**

Keys in SQL are used to uniquely identify records in a table and establish relationships between tables. Below are the main types of keys used in database management systems.

## **1. Super Key**

A super key is a set of one or more attributes that can uniquely identify a row in a table. It may contain extra attributes that are not necessary for uniqueness.

### **Example:**

```sql
(Employee_ID, Name)
```

Here, `Employee_ID` alone can uniquely identify a record, but `Employee_ID, Name` is also a super key.

---
 
## **2. Candidate Key**

A candidate key is a minimal super key, meaning it has no redundant attributes. A table can have multiple candidate keys, but only one can be chosen as the primary key.

### **Example:**

```sql
Employee_ID or Email
```

Both `Employee_ID` and `Email` can uniquely identify a record, so they are candidate keys.

---

## **3. Difference Between Super Key and Candidate Key**

- **Super Key**: Can have extra attributes that are not necessary for uniqueness.
- **Candidate Key**: A minimal super key with no extra attributes.
- **All candidate keys are super keys, but not all super keys are candidate keys.**

### **Subset Diagram:**

```
Super Key ⊃ Candidate Key ⊃ Primary Key
```

Candidate keys are a subset of super keys, and the primary key is one selected candidate key.

---

## **4. Primary Key**

A primary key is a candidate key that has been selected to uniquely identify records in a table. It ensures uniqueness and does not allow NULL values.

### **Example:**

```sql
CREATE TABLE Employees (
    Employee_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE
);
```

Here, `Employee_ID` is the primary key.

---

## **5. Alternate Key**

An alternate key is a candidate key that is not selected as the primary key. It can still uniquely identify records but is not used as the main key.

### **Example:**

```sql
Email (if Employee_ID is the primary key)
```

Here, `Email` is an alternate key because it was not chosen as the primary key.

---

## **6. Foreign Key**

A foreign key is an attribute in one table that references the primary key of another table. It helps maintain referential integrity between related tables.

### **Example:**

```sql
CREATE TABLE Orders (
    Order_ID INT PRIMARY KEY,
    Employee_ID INT,
    FOREIGN KEY (Employee_ID) REFERENCES Employees(Employee_ID)
);
```

Here, `Employee_ID` in the `Orders` table is a foreign key referencing `Employee_ID` in the `Employees` table.

These keys play a crucial role in ensuring data integrity and efficient database design.


### **Composite Key in SQL**

A **composite key** is a **combination of two or more columns** that uniquely identify a row in a table. Unlike a **primary key**, which can be a single column, a composite key consists of **multiple columns** because a single column alone is not sufficient to ensure uniqueness.

---

### **Key Properties of Composite Key**

✅ **Uniqueness** – The combination of values in the key columns must be unique across all rows.  
✅ **Multiple Columns** – At least **two** columns form the key.  
✅ **Can Contain Candidate Keys** – A composite key can be a candidate key if it is unique and does not allow NULL values.

![[Pasted image 20250216192620.png]]


