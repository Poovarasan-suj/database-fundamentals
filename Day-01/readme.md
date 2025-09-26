

##  Database Basics

* **Database** → Collection of organized data.
* **DBMS (Database Management System)** → Software to manage data. (MySQL, PostgreSQL, Oracle, SQL Server).
* **RDBMS (Relational DBMS)** → Data stored in **tables** (rows & columns). MySQL is an RDBMS.

---

##  SQL Basics

* **SQL (Structured Query Language)** = Language to communicate with databases.
* Common operations:

  * `CREATE` → Databases/Tables
  * `INSERT` → Add data
  * `SELECT` → Query data
  * `UPDATE` → Modify data
  * `DELETE` → Remove data

---

##  MySQL Installation (Rocky Linux)

```bash
# Install MySQL repo & server
sudo dnf install mysql-community-server -y

# Start and enable service
sudo systemctl start mysqld
sudo systemctl enable mysqld

# Get temporary root password
sudo grep 'temporary password' /var/log/mysqld.log

# Secure installation (set root password, remove test DB, etc.)
sudo mysql_secure_installation
```

---

## MySQL CLI Basics

```sql
-- Login
mysql -u root -p

-- Show all databases
SHOW DATABASES;

-- Create a new database
CREATE DATABASE school_db;

-- Select database to use
USE school_db;
```

---

##  Tables

```sql
-- Create table
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(25),
    city VARCHAR(10),
    gpa DECIMAL(3,2)
);

-- Show table structure
DESCRIBE students;
```

---

##  Insert Data

```sql
-- Insert single row
INSERT INTO students VALUES (1, 'Poovarasan', 'Chennai', 9.05);

-- Insert multiple rows
INSERT INTO students (id, name, city, gpa)
VALUES
(2, 'Alice', 'Delhi', 8.50),
(3, 'Bob', 'Mumbai', 7.20);
```

---

##  Select Data

```sql
-- Select all rows
SELECT * FROM students;

-- Select specific columns
SELECT name, gpa FROM students;
```

---

## Key Learnings

* SQL commands end with **semicolon `;`**.
* Strings must be inside **quotes `' '`**.
* If MySQL shows `->`, it means command is not finished yet.
* **Primary Key** → Unique identifier for each row.
* **Data Types**:

  * `INT` → numbers
  * `VARCHAR(n)` → text up to n characters
  * `DECIMAL(p,s)` → fixed-point numbers

---




