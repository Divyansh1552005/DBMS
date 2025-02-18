# **SQL Operators in MySQL**

## **1. DISTINCT**

DISTINCT is used to remove duplicate values from a result set. When retrieving data from a column, it ensures that only unique values appear in the output.

### **Syntax:**

```sql
SELECT DISTINCT column_name FROM table_name;
```

### **Example:**

```sql
SELECT DISTINCT department FROM Employees;
```

## **2. LIKE (Pattern Matching)**

LIKE is used for pattern matching within a column. It allows searching for values that match a specific pattern using wildcard characters like `%` (matches any number of characters) and `_` (matches a single character).

### **Syntax:**

```sql
SELECT * FROM table_name WHERE column_name LIKE 'pattern';
```

### **Example:**

```sql
SELECT * FROM Employees WHERE Name LIKE 'A%';
```

## **3. IN (Multiple Value Match)**

IN is used to filter results by matching a column’s value against multiple specified values. It is a more concise way to use multiple OR conditions.

### **Syntax:**

```sql
SELECT * FROM table_name WHERE column_name IN (value1, value2, ...);
```

### **Example:**

```sql
SELECT * FROM Employees WHERE department IN ('HR', 'IT');
```

## **4. BETWEEN (Range Selection)**

BETWEEN is used to filter results within a specified range of values. It is inclusive, meaning it includes both the start and end values in the range.

### **Syntax:**

```sql
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
```

### **Example:**

```sql
SELECT * FROM Employees WHERE Salary BETWEEN 30000 AND 60000;
```

## **5. EXISTS (Subquery Check)**

EXISTS is used to check whether a subquery returns any rows. If the subquery returns at least one row, the EXISTS condition evaluates to TRUE.

### **Syntax:**

```sql
SELECT column_name FROM table1 WHERE EXISTS (SELECT * FROM table2 WHERE condition);
```
isme top to down appraoch use karte hai rather than bottom to up in IN Query ie in query mein pehle sub-query execute hoti hai and then outer query but isme aisa nahi hota.
### **Example:**

```sql
SELECT Name FROM Employees WHERE EXISTS (SELECT * FROM Departments WHERE Employees.Department = Departments.Name);
```

## **6. NOT EXISTS (Negated Subquery Check)**

NOT EXISTS is used to check whether a subquery returns no rows. If the subquery does not return any rows, the condition evaluates to TRUE, effectively filtering out certain records.

### **Syntax:**

```sql
SELECT column_name FROM table1 WHERE NOT EXISTS (SELECT * FROM table2 WHERE condition);
```

### **Example:**

```sql
SELECT Name FROM Employees WHERE NOT EXISTS (SELECT * FROM Projects WHERE Employees.ID = Projects.EmployeeID);
```


## Aliases in table

![[Pasted image 20250216143948.png]]


[[5 SQL Aggregate functions]]
