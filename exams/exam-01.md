# Exam 1 - Database Fundamentals

## Date
[Add exam date here]

## Questions

### Question 1: Database Normalization
Explain the first three normal forms (1NF, 2NF, 3NF) and provide an example of a table that violates 2NF, showing how to normalize it.

### Question 2: SQL Queries
Given the following schema:
```sql
Students (student_id, name, email, major)
Courses (course_id, course_name, credits)
Enrollments (enrollment_id, student_id, course_id, grade, semester)
```

Write SQL queries for:
a) List all students enrolled in courses during Fall 2024
b) Calculate the average grade per course
c) Find students who are enrolled in more than 3 courses

### Question 3: Transactions and ACID
Explain the ACID properties of database transactions and provide a practical example where each property is critical.

---

## Resolution

### Answer to Question 1: Database Normalization

**First Normal Form (1NF):**
- Each column contains atomic values
- No repeating groups
- Each row is unique

**Second Normal Form (2NF):**
- Must be in 1NF
- All non-key attributes must be fully dependent on the primary key
- No partial dependencies

**Third Normal Form (3NF):**
- Must be in 2NF
- No transitive dependencies
- Non-key attributes depend only on the primary key

**Example of 2NF Violation:**

Original table (violates 2NF):
```
StudentCourse (student_id, course_id, student_name, course_name, grade)
Primary Key: (student_id, course_id)
```

Problem: `student_name` depends only on `student_id` (partial dependency), and `course_name` depends only on `course_id` (partial dependency).

**Normalized to 2NF:**
```
Students (student_id, student_name)
Courses (course_id, course_name)
Enrollments (student_id, course_id, grade)
```

### Answer to Question 2: SQL Queries

**a) List all students enrolled in courses during Fall 2024:**
```sql
SELECT DISTINCT s.student_id, s.name, s.email
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
WHERE e.semester = 'Fall 2024';
```

**b) Calculate the average grade per course:**
```sql
SELECT c.course_id, c.course_name, AVG(e.grade) AS average_grade
FROM Courses c
JOIN Enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name;
```

**c) Find students who are enrolled in more than 3 courses:**
```sql
SELECT s.student_id, s.name, COUNT(e.course_id) AS course_count
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.name
HAVING COUNT(e.course_id) > 3;
```

### Answer to Question 3: Transactions and ACID

**ACID Properties:**

1. **Atomicity**: All operations in a transaction succeed or all fail
   - Example: Bank transfer - both debit and credit must complete or neither should

2. **Consistency**: Transaction brings database from one valid state to another
   - Example: Account balance constraints must be maintained (no negative balances)

3. **Isolation**: Concurrent transactions don't interfere with each other
   - Example: Two users booking the last seat on a flight shouldn't both succeed

4. **Durability**: Once committed, changes persist even after system failure
   - Example: After payment confirmation, the transaction record must survive a crash

**Practical Example - Banking Transaction:**
```sql
BEGIN TRANSACTION;

-- Atomicity: Both operations must complete
UPDATE accounts SET balance = balance - 100 WHERE account_id = 'A123';
UPDATE accounts SET balance = balance + 100 WHERE account_id = 'B456';

-- Consistency: Check constraints are maintained
-- Isolation: Other transactions can't see intermediate state
-- Durability: Changes are written to persistent storage

COMMIT;
```

If any step fails, the entire transaction is rolled back, ensuring data integrity.
