
# MySQL JOINS - Detailed Notes

---
Study from nb notes too.

## 📚 What is a JOIN?

In SQL, **JOIN** is used to combine rows from two or more tables based on a related column between them.

> Joins help in fetching meaningful combined data from multiple tables.

---

## 🛠 Types of JOINS

---

### 1. INNER JOIN 

- **Returns** only the matching rows from both tables.
- **If no match is found**, that row is **not included**.


**Syntax:**

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:** Suppose we have two tables:

**Employees Table:**

|id|name|department_id|
|---|---|---|
|1|Alice|101|
|2|Bob|102|
|3|Charlie|NULL|

**Departments Table:**

|id|department_name|
|---|---|
|101|HR|
|102|IT|
|103|Finance|

Query:

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
INNER JOIN Departments
ON Employees.department_id = Departments.id;
```

**Result:**

|name|department_name|
|---|---|
|Alice|HR|
|Bob|IT|

Only those employees appear who have a matching department.

Note - 
- **Equi Join** koi **algebraic join type nahi** hai MySQL mein.
- **Equi Join** = **INNER JOIN with `=` operator** used.
- Matlab har **INNER JOIN** jisme hum `=` se match karte hain, woh ek **Equi Join** hai.

---

### 2. LEFT JOIN (LEFT OUTER JOIN)

- **Returns** all records from the **left** table and matching records from the right table.
- **If no match**, NULLs are shown for right table columns.

**Syntax:**

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:** Query:

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
LEFT JOIN Departments
ON Employees.department_id = Departments.id;
```

**Result:**

|name|department_name|
|---|---|
|Alice|HR|
|Bob|IT|
|Charlie|NULL|

All employees appear. Charlie has no department, so department_name is NULL.

---

### 3. RIGHT JOIN (RIGHT OUTER JOIN)

- **Returns** all records from the **right** table and matching records from the left table.
    
- **If no match**, NULLs are shown for left table columns.
    

**Syntax:**

```sql
SELECT table1.column1, table2.column2
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:** Query:

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
RIGHT JOIN Departments
ON Employees.department_id = Departments.id;
```

**Result:**

|name|department_name|
|---|---|
|Alice|HR|
|Bob|IT|
|NULL|Finance|

Even though no employee belongs to Finance, Finance still appears.

---

### 4. FULL JOIN (FULL OUTER JOIN)

- **Returns** all records when there is a match in **either** left or right table.
- **Non-matching rows** are filled with NULLs.
- **Note:** MySQL doesn't support FULL JOIN directly. You have to **simulate it** using `UNION`.

**Syntax (Simulated FULL JOIN):**

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column

UNION

SELECT table1.column1, table2.column2
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:** Query:

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
LEFT JOIN Departments
ON Employees.department_id = Departments.id

UNION

SELECT Employees.name, Departments.department_name
FROM Employees
RIGHT JOIN Departments
ON Employees.department_id = Departments.id;
```

**Result:**

|name|department_name|
|---|---|
|Alice|HR|
|Bob|IT|
|Charlie|NULL|
|NULL|Finance|

All data is combined.

---

### 5. CROSS JOIN

- **Returns** the **Cartesian product** of two tables.
    
- Every row of table1 is paired with every row of table2.
    
- **No ON condition**.
    

**Syntax:**

```sql
SELECT table1.column1, table2.column2
FROM table1
CROSS JOIN table2;
```

**Example:** Query:

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
CROSS JOIN Departments;
```

If Employees has 3 rows and Departments has 2 rows: Total rows = 3 * 2 = 6 rows.

|name|department_name|
|---|---|
|Alice|HR|
|Alice|IT|
|Bob|HR|
|Bob|IT|
|Charlie|HR|
|Charlie|IT|

---

### 6. SELF JOIN

- A table is **joined with itself**.
    
- Useful for hierarchical data (manager-employee relations).
    

**Syntax:**

```sql
SELECT A.name AS Employee, B.name AS Manager
FROM Employees A
LEFT JOIN Employees B
ON A.manager_id = B.id;
```

**Example:** Suppose:

|id|name|manager_id|
|---|---|---|
|1|Alice|NULL|
|2|Bob|1|
|3|Charlie|1|
|4|David|2|

Query:

```sql
SELECT A.name AS Employee, B.name AS Manager
FROM Employees A
LEFT JOIN Employees B
ON A.manager_id = B.id;
```

**Result:**

|Employee|Manager|
|---|---|
|Alice|NULL|
|Bob|Alice|
|Charlie|Alice|
|David|Bob|


##  7. 📚 What is NATURAL JOIN?

- **NATURAL JOIN** is a type of join where MySQL automatically joins two tables **based on all columns with the same name** and **compatible data types**.
    
- You **don't have to specify** the join condition manually.
    
- **Duplicate columns** from the result set are **eliminated** automatically.
    

> NATURAL JOIN is basically a shortcut for an INNER JOIN where MySQL guesses the matching columns.

---

## 🛠 Syntax

```sql
SELECT column_list
FROM table1
NATURAL JOIN table2;
```

- No need for an `ON` condition.
- If multiple columns have the same name, all are used for joining.

---

## 👨‍👩‍👦 Example

Suppose we have two tables:

**Employees Table:**

|emp_id|name|department_id|
|---|---|---|
|1|Alice|101|
|2|Bob|102|
|3|Carol|103|

**Departments Table:**

|department_id|department_name|
|---|---|
|101|HR|
|102|IT|
|104|Finance|

### Query using NATURAL JOIN:

```sql
SELECT name, department_name
FROM Employees
NATURAL JOIN Departments;
```

- MySQL automatically matches `department_id` because it exists in both tables.
      
- Only employees with matching department_ids will appear.
    

**Result:**

|name|department_name|
|---|---|
|Alice|HR|
|Bob|IT|

Carol is excluded because her department_id (103) has no match in Departments table.

---

## 🔍 Important Points

- NATURAL JOIN works like an INNER JOIN.
    
- It **fails** or **gives wrong results** if common column names are missing or wrong.
    
- If there are multiple columns with the same name, NATURAL JOIN will use all of them for matching.
    
- Best practice is to avoid NATURAL JOIN in complex queries for better readability and control.
    

---

## 📈 Visual Representation

|Employees.department_id|Departments.department_id|
|:--|:--|
|101|101|
|102|102|
|103|(no match)|

NATURAL JOIN matches only where IDs are common.

---

## ⏳ Time Complexity

- Theoretically similar to INNER JOIN: **O(N \u00d7 M)** in the worst case.
- Practical performance depends heavily on indexes.

---

# 💡 Final Notes

> "**NATURAL JOIN automatically figures out the JOIN condition for you based on same column names.**"

But be careful: **Explicit INNER JOIN is preferred** in real-world large applications for clarity and maintainability.

---

## 📈 Visual Diagrams

|JOIN Type|Visual|
|:--|:--|
|INNER JOIN|Intersection only|
|LEFT JOIN|All left + matching right|
|RIGHT JOIN|All right + matching left|
|FULL JOIN|All data from both sides|
|CROSS JOIN|All combinations|

(You can draw Venn diagrams for better memory.)

---

## ⏳ Time Complexity (Theoretical)

- Joins are internally optimized by SQL engine.
    
- Worst-case can be **O(N × M)** for naive joins.
    
- Indexing **common columns** can significantly improve performance.
    

---

# 📜 Example Problem

**Problem:**  
List all employees with their department names. Show "No Department" if not assigned.

**Solution:**

```sql
SELECT e.name, 
       IFNULL(d.department_name, 'No Department') AS department_name
FROM Employees e
LEFT JOIN Departments d
ON e.department_id = d.id;
```

---


[[10 TCL Commands]]

