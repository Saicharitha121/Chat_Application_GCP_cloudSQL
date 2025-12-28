# Student Management System using Google Cloud SQL

##  Project Overview

This project demonstrates how to build a simple **Student Management
System** using **Google Cloud SQL**.
It covers database creation, table design, data insertion, querying, and
securing the database using best practices.

The goal of this small task is to showcase **Cloud SQL setup, SQL
fundamentals, and basic networking & security skills**.

------------------------------------------------------------------------

## Technologies Used

-   Google Cloud Platform (GCP)
-   Cloud SQL (MySQL)
-   SQL
-   Cloud IAM & Networking


------------------------------------------------------------------------

##  Implementation Steps

### 1. Create Cloud SQL Instance

-   Created a Cloud SQL instance on GCP
-   Selected database engine: MySQL 
-   Configured region and zone
-   Enabled public IP for connectivity

------------------------------------------------------------------------

### 2️. Create Database

``` sql
CREATE DATABASE college_db;
```

------------------------------------------------------------------------

### 3️. Create `students` Table

``` sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    marks INT
);
```

------------------------------------------------------------------------

### 4️. Insert Sample Records

``` sql
INSERT INTO students (student_id, name, department, marks) VALUES
(1, 'Ananya', 'CSE', 88),
(2, 'charitha', 'ECE', 72),
(3, 'Sai', 'CSE', 91),
(4, 'varun', 'MECH', 65),
(5, 'sneha', 'ECE', 79);
```

------------------------------------------------------------------------

##  SQL Queries

###  Fetch students with marks \> 75

``` sql
SELECT * FROM students
WHERE marks > 75;
```

------------------------------------------------------------------------

###  Count students per department

``` sql
SELECT department, COUNT(*) AS student_count
FROM students
GROUP BY department;
```

------------------------------------------------------------------------


###  Restrict Access to Specific IP

-   Configured Authorized Networks in Cloud SQL
-   Allowed access only from a specific IP address
-   Ensured no unrestricted public access


------------------------------------------------------------------------

