# **Foreign Key & Referential Integrity**


To understand more, watch this - 
<iframe width="560" height="315" src="https://www.youtube.com/embed/DM2lAomoDrg?si=smvC2rcM2oHdBoA6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
Note write better notes for this later.

## **1. What is a Foreign Key?**

A **Foreign Key (FK)** is a column (or a set of columns) in a table that establishes a relationship between two tables. It references the **Primary Key (PK)** of another table to enforce data consistency and integrity.

### **Example:**

Consider two tables:

- **`Students` (StudentID as Primary Key)**
- **`Enrollments` (EnrollmentID as Primary Key, StudentID as Foreign Key referencing `Students`)**

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100)
);

CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseName VARCHAR(100),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);
```

### **Adding a Foreign Key using ALTER TABLE**

If the `Enrollments` table is already created without a foreign key, we can add it later using `ALTER TABLE`:

```sql
ALTER TABLE Enrollments
ADD CONSTRAINT fk_student FOREIGN KEY (StudentID) REFERENCES Students(StudentID);
```

---

## **2. Referential Integrity**

**Referential Integrity** ensures that the relationship between tables remains valid:

- A Foreign Key **must reference an existing Primary Key** or be NULL.
- Prevents **orphan records** (e.g., an enrollment without a valid student).

If referential integrity is not maintained, the following issues can occur:

1. **Insertion Issue:** Trying to insert a record in the referencing table (`Enrollments`) with a `StudentID` that does not exist in `Students` will fail.
2. **Deletion Issue:** Deleting a record from the reference table (`Students`) without handling dependent records in `Enrollments` will break the link.
3. **Update Issue:** Changing a Primary Key in the reference table without updating corresponding Foreign Keys will cause inconsistency.

---

## **3. Reference Table vs Referencing Table**

|Concept|Description|
|---|---|
|**Reference Table**|The table containing the **Primary Key** (e.g., `Students`).|
|**Referencing Table**|The table containing the **Foreign Key** (e.g., `Enrollments`).|

---

## **4. INSERT Operations**

### **Inserting into Reference Table (Students)**

```sql
INSERT INTO Students (StudentID, Name) VALUES (1, 'Alice');
INSERT INTO Students (StudentID, Name) VALUES (2, 'Bob');
```
Base table mein jitna insert kardo no problem.
### **Inserting into Referencing Table (Enrollments)**

```sql
INSERT INTO Enrollments (EnrollmentID, StudentID, CourseName) VALUES (101, 1, 'Math');
INSERT INTO Enrollments (EnrollmentID, StudentID, CourseName) VALUES (102, 2, 'Science');
```

✅ **Valid Insert:** StudentID `1` and `2` exist in `Students`.  
❌ **Invalid Insert:** `INSERT INTO Enrollments VALUES (103, 3, 'History');` (Fails if StudentID `3` does not exist in `Students`).

---

## **5. DELETE Operations**

### **Deleting from Reference Table (Students)**

- If **no constraints**, deleting a student **breaks referential integrity** because existing enrollments reference that student.
- To enforce referential integrity, use **ON DELETE CASCADE** or **ON DELETE SET NULL**.
 
#### **ON DELETE CASCADE** (Deletes related enrollments automatically)

When this constraint is used, deleting a row from the reference table (`Students`) **automatically deletes all related rows** in the referencing table (`Enrollments`). This prevents orphaned records.

```sql
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseName VARCHAR(100),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID) ON DELETE CASCADE
);
DELETE FROM Students WHERE StudentID = 1; -- Also deletes Alice's enrollments
```

**Why?** Because without `ON DELETE CASCADE`, deleting Alice from `Students` would leave enrollments referring to a non-existing student, violating referential integrity.

#### **ON DELETE SET NULL** (Keeps enrollments but sets StudentID to NULL)

With this setting, when a referenced student is deleted, the foreign key values in `Enrollments` are set to `NULL` instead of removing the rows.

```sql
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseName VARCHAR(100),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID) ON DELETE SET NULL
);
DELETE FROM Students WHERE StudentID = 1; -- Sets StudentID in Enrollments to NULL
```

**Why?** This is useful when we want to retain enrollment records even if the student is removed.

---

## **6. UPDATE Operations**

### **Updating Primary Key in Reference Table (Students)**

- Directly updating a Primary Key **without cascading changes** may cause foreign key violations.
- **ON UPDATE CASCADE** allows automatic updates in the referencing table.

#### **ON UPDATE CASCADE** (Updates the Foreign Key automatically)

With this setting, if the primary key in the reference table is updated, all corresponding foreign keys in the referencing table are updated automatically.

```sql
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseName VARCHAR(100),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID) ON UPDATE CASCADE
);
UPDATE Students SET StudentID = 10 WHERE StudentID = 1; -- Updates Enrollments too
```

**Why?** Without `ON UPDATE CASCADE`, changing `StudentID` in `Students` would leave `Enrollments` with invalid references, breaking referential integrity.

---

This detailed explanation ensures a complete understanding of how foreign keys, referential integrity, and cascading operations work in relational databases.

Note that learn from notebook about updating tables through foreign key or by gate smashers.



[[8 one compiler se pdho Single row functions]]

