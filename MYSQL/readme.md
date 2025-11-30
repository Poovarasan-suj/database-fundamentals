# SQL Foundations – Complete Beginner Guide 

##  1. **What is a Database?**

A **database** is a place where data is stored in an organised way.
Think of it like a **digital notebook**.

---

##  2. **What is a Table?**

A **table** is like an Excel sheet inside the database.

* Rows → records (each entry)
* Columns → fields (name, age, city)

---

##  3. **What is a Primary Key?**

A **unique identifier** for each row.

* No duplicates
* Cannot be NULL

Example: `id` in the students table.

---

##  4. **What is a Foreign Key?**

A foreign key **connects two tables**.
It is like saying:

> “This course belongs to this student.”

Example:

* `students.id` → primary key
* `courses.student_id` → foreign key

---

##  5. **What is DISTINCT?**

Removes duplicates.

Example:

```sql
SELECT DISTINCT city FROM students;
```

This shows each city only once.

---

##  6. **What is WHERE?**

Used to filter rows.

Example:

```sql
SELECT * FROM students WHERE age > 25;
```

Shows only students whose age is above 25.

---

##  7. **What is ORDER BY?**

Sorts results.

* ASC → ascending
* DESC → descending

Example:

```sql
SELECT * FROM students ORDER BY age DESC;
```

---

##  8. **What is LIMIT?**

Shows only limited number of rows.

Example:

```sql
SELECT * FROM students LIMIT 3;
```

---

#  JOINs (Explained in the Easiest Way)

JOINs connect data from two tables.

##  9. **What is INNER JOIN?**

Shows **only matching data** from both tables.

Meaning:

> “Show students who have courses.”

---

##  10. **What is LEFT JOIN?**

Shows **all students**, even if they don’t have a course.

Meaning:

> “Show every student. If they don’t have a course, show NULL.”

---

##  11. **What is RIGHT JOIN?**

Shows **all courses**, even if student does not exist.

Meaning:

> “Show every course. If no student matches, show NULL.”

---

#  GROUPING Concepts

##  12. **What is GROUP BY?**

Used to group rows by a column.

Meaning:

> "Group all students based on their city."

Example:

```sql
SELECT city, COUNT(*) FROM students GROUP BY city;
```

---

## 13. **What is HAVING?**

This is very important.

### WHERE → filters **rows** before grouping

### HAVING → filters **groups** after grouping

Meaning:

> “Show only groups that meet a condition.”

Example:

```sql
SELECT city, COUNT(*) FROM students GROUP BY city HAVING COUNT(*) > 2;
```

---

#  Subqueries

A **subquery** is a SELECT inside another SELECT.

## ⭐ 14. **What is a Subquery?**

Meaning:

> “A small query used inside a bigger query.”

Used when:

* you need a calculated value (like average age)
* you want to filter using that value

### Example (inside SELECT):

```sql
SELECT name, age, (SELECT AVG(age) FROM students) AS average_age FROM students;
```

Meaning:

> “Show each student and also show the average age.”

### Example (inside WHERE):

```sql
SELECT name FROM students WHERE age > (SELECT AVG(age) FROM students);
```

Meaning:

> “Show students older than average age.”

---

#  15. What Are Constraints?

Constraints make rules for columns.

| Constraint  | Meaning                       |
| ----------- | ----------------------------- |
| PRIMARY KEY | Row must be unique            |
| NOT NULL    | Value cannot be empty         |
| UNIQUE      | No duplicate values           |
| DEFAULT     | Auto fill value               |
| CHECK       | Validate value (ex: age > 18) |
| FOREIGN KEY | Connect tables                |

---

#  16. What is a MySQL User?

A separate login for accessing the database.

Meaning:

> “Create a user for developers with limited permissions.”

Example:

```sql
CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'Password123';
```

Grant permissions:

```sql
GRANT ALL PRIVILEGES ON company_db.* TO 'devuser'@'localhost';
```

---

#  17. What is Backup and Restore?

A backup saves your database to a file.
Restore loads it back.

### Backup:

```bash
mysqldump -u root -p company_db > backup.sql
```

### Restore:

```bash
mysql -u root -p company_db < backup.sql
```

---

#  Final Summary

* **Database** = place to store data
* **Table** = like Excel sheet
* **Primary Key** = unique row ID
* **Foreign Key** = link between tables
* **WHERE** = filter rows
* **ORDER BY** = sort
* **LIMIT** = restrict rows
* **JOINs** = combine tables
* **GROUP BY** = group data
* **HAVING** = filter groups
* **SUBQUERY** = query inside query
* **DISTINCT** = remove duplicates
* **MySQL User** = separate DB login
* **Backup** = save database to file

This section now explains every concept clearly for beginners. – Complete Beginner Guide (Cloud Engineer Friendly)


---

# 📘 What This Document Covers

* What is SQL?
* How to install MySQL on Linux (Rocky/Ubuntu)
* How to start & use MySQL
* How to create a database
* How to create tables
* How to view databases, tables, and data
* How to insert, update, delete rows
* Filtering (WHERE)
* Sorting (ORDER BY)
* Limiting results (LIMIT)
* JOINS (INNER, LEFT, RIGHT)
* GROUP BY + HAVING
* Subqueries made simple
* DISTINCT, constraints, foreign keys
* Creating MySQL users
* Granting permissions
* Backup & Restore (mysqldump)



---

# 🧩 1. What is SQL?

SQL (Structured Query Language) is a language used to store, retrieve, and manage data in databases.

Examples: MySQL, MariaDB, PostgreSQL, Oracle, SQL Server.

---

# 🛠 2. Installing MySQL on Linux (Rocky Linux / RHEL / CentOS)

### Step 1: Add MySQL repo (for MySQL 8)

```bash
sudo dnf install https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
```

### Step 2: Install MySQL Server

```bash
sudo dnf install mysql-community-server -y
```

### Step 3: Start MySQL service

```bash
sudo systemctl start mysqld
sudo systemctl enable mysqld
```

### Step 4: Login

```bash
sudo mysql -u root -p
```

(Use the temporary password if required.)

---

# 3. Basic MySQL Commands

### Show all databases

```sql
SHOW DATABASES;
```

### Use a database

```sql
USE database_name;
```

### Show all tables in current database

```sql
SHOW TABLES;
```

### Describe a table

```sql
DESCRIBE table_name;
```

---

#  4. Creating a Database

```sql
CREATE DATABASE company_db;
```

Select the DB:

```sql
USE company_db;
```

---

#  5. Creating a Table

### Example: Students table

```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    age INT,
    city VARCHAR(50)
);
```

---

#  6. Insert Data into the Table

```sql
INSERT INTO students (name, age, city)
VALUES
("Ravi", 25, "Chennai"),
("Priya", 22, "Madurai"),
("Kumar", 28, "Coimbatore");
```

---

#  7. Selecting Data

### Select all rows

```sql
SELECT * FROM students;
```

### Select specific columns

```sql
SELECT name, city FROM students;
```

---

#  8. Filtering With WHERE

```sql
SELECT * FROM students WHERE city = 'Chennai';
SELECT * FROM students WHERE age > 25;
SELECT * FROM students WHERE city = 'Chennai' AND age > 20;
```

---

#  9. Sorting Results (ORDER BY)

```sql
SELECT * FROM students ORDER BY age;          -- ascending
SELECT * FROM students ORDER BY age DESC;     -- descending
```

---

# 10. Limiting Results (LIMIT)

```sql
SELECT * FROM students LIMIT 3;
```

---

#  11. JOINS (Very Important)

Joins combine data from multiple tables.

## INNER JOIN – only matching rows

```sql
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses
ON students.id = courses.student_id;
```

## LEFT JOIN – all students + matching courses

```sql
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses
ON students.id = courses.student_id;
```

## RIGHT JOIN – all courses + matching students

```sql
SELECT students.name, courses.course_name
FROM students
RIGHT JOIN courses
ON students.id = courses.student_id;
```

---

#  12. GROUP BY (Summaries)

```sql
SELECT city, COUNT(*) AS total_students
FROM students
GROUP BY city;
```

---

#  13. HAVING (Filter after grouping)

```sql
SELECT city, COUNT(*) AS total_students
FROM students
GROUP BY city
HAVING COUNT(*) > 2;
```

---

#  14. Subqueries (Simple Explanation)

## Subquery in SELECT

```sql
SELECT name, age,
 (SELECT AVG(age) FROM students) AS average_age
FROM students;
```

## Subquery in WHERE

```sql
SELECT name, age
FROM students
WHERE age > (SELECT AVG(age) FROM students);
```

---

#  15. DISTINCT (Remove duplicates)

```sql
SELECT DISTINCT city FROM students;
```

---

#  16. Constraints (Beginner Explanation)

| Constraint  | Meaning                 |
| ----------- | ----------------------- |
| PRIMARY KEY | Unique row identifier   |
| NOT NULL    | Value cannot be empty   |
| UNIQUE      | No duplicates allowed   |
| DEFAULT     | Auto-fill value         |
| CHECK       | Validate values         |
| FOREIGN KEY | Link between two tables |

---

#  17. Foreign Key Example (Concept Only)

```sql
CREATE TABLE courses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_name VARCHAR(50),
    FOREIGN KEY (student_id) REFERENCES students(id)
);
```

---

#  18. Creating a MySQL User

```sql
CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'Password123';
```

### Grant permissions

```sql
GRANT ALL PRIVILEGES ON company_db.* TO 'devuser'@'localhost';
FLUSH PRIVILEGES;
```

---

#  19. Backup and Restore

## Backup a database

```bash
mysqldump -u root -p company_db > company_db_backup.sql
```

## Restore a database

```bash
mysql -u root -p company_db < company_db_backup.sql
```

----------



