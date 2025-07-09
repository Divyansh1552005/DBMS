# **SQL Aggregate Functions**

Aggregate functions in SQL perform calculations on multiple rows of a table and return a single value. These functions are often used with the `GROUP BY` clause to perform operations on groups of data.

## **1. COUNT()**

Counts the number of rows that match a specified condition.

### **Syntax:**

```sql
SELECT COUNT(column_name) FROM table_name WHERE condition;
```

### **Example:**

```sql
SELECT COUNT(*) FROM Employees WHERE Department = 'IT';
```

## **2. SUM()**

Returns the total sum of a numeric column.

### **Syntax:**

```sql
SELECT SUM(column_name) FROM table_name WHERE condition;
```

### **Example:**

```sql
SELECT SUM(Salary) FROM Employees WHERE Department = 'Finance';
```

## **3. AVG()**

Returns the average value of a numeric column.

### **Syntax:**

```sql
SELECT AVG(column_name) FROM table_name WHERE condition;
```

### **Example:**

```sql
SELECT AVG(Salary) FROM Employees WHERE Department = 'HR';
```

## **4. MAX()**

Returns the maximum value in a column.

### **Syntax:**

```sql
SELECT MAX(column_name) FROM table_name WHERE condition;
```

### **Example:**

```sql
SELECT MAX(Salary) FROM Employees;
```

## **5. MIN()**

Returns the minimum value in a column.

### **Syntax:**

```sql
SELECT MIN(column_name) FROM table_name WHERE condition;
```

### **Example:**

```sql
SELECT MIN(Salary) FROM Employees;
```

## **6. GROUP BY with Aggregate Functions**

The `GROUP BY` clause is used to group rows that have the same values in specified columns and perform aggregate functions on these groups.

### **Syntax:**

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name) FROM table_name GROUP BY column_name;
```
group by ke baad vala colmname hi select k baad likh skte ho , aur koi nahi becoz group karne k baad aur chizo ko sense nahi banega think about it.

### **Example:**

```sql
SELECT Department, AVG(Salary) FROM Employees GROUP BY Department;
```

## **7. HAVING Clause with Aggregate Functions**

The `HAVING` clause is used to filter the results of aggregate functions after the `GROUP BY` operation.

### **Syntax:**

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name) FROM table_name GROUP BY column_name HAVING condition;
```

### **Example:**

```sql
SELECT Department, COUNT(*) FROM Employees GROUP BY Department HAVING COUNT(*) > 5;
```

These aggregate functions are essential in SQL for summarizing and analyzing data efficiently.


## **Using `LIMIT` with `ORDER BY`**

The `LIMIT` clause in SQL is used to restrict the number of rows returned in the result set. When combined with `ORDER BY`, it helps in selecting the **top** or **bottom** values based on sorting order.
**Example: Finding the Highest Salary (Top 1)**
```sql
SELECT e_name, salary 
FROM emp 
ORDER BY salary DESC 
LIMIT 1;
```

**Explanation:**

- `ORDER BY salary DESC` → Sorts the salaries in **descending order** (highest first).
- `LIMIT 1` → Retrieves **only the first row** (the highest salary).

## **Finding the Nth Highest Salary**

To find the **Nth highest salary**, we use `LIMIT` with `OFFSET`.
```sql
SELECT salary 
FROM emp 
ORDER BY salary DESC 
LIMIT 1 OFFSET N-1;
```
🔹 `OFFSET N-1` skips the first `(N-1)` rows and selects the Nth row.


**Example: Finding the 3rd Highest Salary**
```sql
SELECT salary 
FROM emp 
ORDER BY salary DESC 
LIMIT 1 OFFSET 2;
```

Note that if duplicate salary exists use distinct in above.

 ![[Pasted image 20250216145448.png]]

# **Types of SQL Queries**

## **1. Simple Query (Single-Level Query)**

A simple query is a basic `SELECT` statement used to retrieve data from a table without using subqueries or joins.

### **Example:**

```sql
SELECT e_name, salary
FROM emp
WHERE salary > 50000;
```

🔹 Retrieves all employees whose salary is greater than 50,000.

---

## **2. Nested Subquery (Non-Correlated Subquery)**

A **subquery** (also called an **inner query**) is a query inside another query. A **non-correlated subquery** executes **independently** of the outer query.

### **Example: Find Employees Earning More than the Average Salary**

```sql
SELECT e_name, salary
FROM emp
WHERE salary > (SELECT AVG(salary) FROM emp);
```

🔹 The inner query `(SELECT AVG(salary) FROM emp)` runs **first** and returns the average salary. 🔹 The outer query then selects employees earning more than this value. 🔹 The inner query executes **only once**, making it **faster** than correlated subqueries.

---

## **3. Correlated Subquery**

A **correlated subquery** is a subquery that **depends on the outer query**. It executes **once for each row** in the outer query, making it **slower** than non-correlated subqueries.

### **Example: Find Employees with the Highest Salary in Their Department**

```sql
SELECT e_name, salary, dept_id
FROM emp E1
WHERE salary = (
    SELECT MAX(salary)
    FROM emp E2
    WHERE E1.dept_id = E2.dept_id
);
```

🔹 The inner query depends on each row of the outer query (`E1.dept_id = E2.dept_id`). 🔹 The inner query runs **multiple times**—once for each department. 🔹 **Correlated subqueries are slower** because they execute repeatedly for each row in the outer query.

---

## **4. EXISTS and NOT EXISTS (Checking for Existence)**

The `EXISTS` and `NOT EXISTS` operators are used to check whether a subquery returns any rows.

### **Example: Find Employees Who Belong to a Department**

```sql
SELECT e_name
FROM emp E
WHERE EXISTS (SELECT 1 FROM dept D WHERE E.dept_id = D.dept_id);
```

🔹 The subquery checks if an employee's `dept_id` exists in the `dept` table. 🔹 The `EXISTS` condition stops as soon as it finds a match, making it **efficient** for large datasets.

### **Example: Find Employees Without an Assigned Department**

```sql
SELECT e_name
FROM emp E
WHERE NOT EXISTS (SELECT 1 FROM dept D WHERE E.dept_id = D.dept_id);
```

🔹 Retrieves employees who **don’t have a matching department**.

---

## **5. Common Table Expressions (CTEs)**

A **CTE** (`WITH` clause) is a temporary result set used within a query to improve readability and performance.

### **Example: Find Employees with Above-Average Salaries Using CTE**

```sql
WITH AvgSalary AS (
    SELECT AVG(salary) AS avg_salary FROM emp
)
SELECT e_name, salary
FROM emp, AvgSalary
WHERE emp.salary > AvgSalary.avg_salary;
```

🔹 The **CTE (`AvgSalary`) is calculated first** and then used in the main query. 🔹 **More readable than nested subqueries**.

---

## **Summary Table**

|Query Type|Execution|Example|
|---|---|---|
|**Simple Query**|Single query execution|`SELECT * FROM emp;`|
|**Non-Correlated Subquery**|Inner query executes **once**|`WHERE salary > (SELECT AVG(salary) FROM emp);`|
|**Correlated Subquery**|Inner query runs for **each row** in the outer query|`WHERE salary = (SELECT MAX(salary) FROM emp E2 WHERE E1.dept_id = E2.dept_id);`|
|**EXISTS / NOT EXISTS**|Checks for the existence of rows|`WHERE EXISTS (SELECT 1 FROM dept WHERE emp.dept_id = dept.dept_id);`|
|**Common Table Expressions (CTEs)**|Uses temporary named result set|`WITH AvgSalary AS (...) SELECT * FROM emp, AvgSalary WHERE...;`|
[[6 Different types of keys]]


