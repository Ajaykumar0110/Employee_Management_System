
# 🧾 Employee Management System (SQL Project)

![Made with MySQL](https://img.shields.io/badge/Made%20with-MySQL-blue?style=for-the-badge&logo=mysql)
![Database Project](https://img.shields.io/badge/Project-Type%3A%20Database-green?style=for-the-badge)
![Open Source](https://img.shields.io/badge/Open%20Source-Yes-orange?style=for-the-badge)

> A SQL-based Employee Management System that manages employee data, payroll, leaves, qualifications, and department insights using relational databases and advanced SQL queries for HR analytics.

## 📌 Overview  
The **Employee Management System (EMS)** is a structured **SQL-based project** that streamlines HR data management.  
It enables efficient handling of employee records, payroll, leaves, bonuses, and departmental insights — all within a well-designed relational database.  

This project highlights **SQL concepts** such as normalization, joins, aggregate functions, and referential integrity, helping organizations make **data-driven workforce decisions**.

---

## 🎯 Objective  
To develop a **comprehensive employee database** that:  
- Centralizes employee, department, and payroll data  
- Ensures data integrity through relational structures  
- Generates HR insights from SQL queries  
- Simplifies salary, leave, and performance tracking  

---

## 🧠 ER Diagram Overview  
**Entities:**  
- Employee  
- Qualification  
- JobDepartment  
- Payroll  
- SalaryBonus  

**Relationships:**  
- Employee → Qualification (One-to-Many)  
- Employee → JobDepartment (One-to-One/Many)  
- Employee → Payroll (One-to-Many)  
- Employee → SalaryBonus (One-to-Many)  

---

## 🧩 Database Design  

| Table | Primary Key | Foreign Key | Key Attributes |
|--------|--------------|--------------|----------------|
| **Employee** | emp_ID | - | name, gender, age, contact, email, password |
| **Qualification** | qual_ID | emp_ID | qualification_details, requirements, hire_date |
| **JobDepartment** | dept_ID | emp_ID | department_name, job_description, salary_range |
| **Payroll** | payroll_ID | emp_ID | salary_ID, leave_days, date, report, total_amount |
| **SalaryBonus** | bonus_ID | emp_ID | base_amount, annual_salary, bonus_structure |

---

## ⚙️ Tech Stack
- **Database:** MySQL 
- **Language:** SQL  

---

## 🚀 Project Setup

### 1️⃣ Create the Database
```sql
CREATE DATABASE EmployeeManagementSystem;
USE EmployeeManagementSystem;
````

### 2️⃣ Create Tables

```sql
CREATE TABLE Employee (
  emp_ID INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(50),
  gender VARCHAR(10),
  age INT,
  contact VARCHAR(20),
  email VARCHAR(100) UNIQUE,
  password VARCHAR(50)
);

CREATE TABLE Qualification (
  qual_ID INT PRIMARY KEY AUTO_INCREMENT,
  emp_ID INT,
  qualification_details VARCHAR(100),
  requirements VARCHAR(100),
  hire_date DATE,
  FOREIGN KEY (emp_ID) REFERENCES Employee(emp_ID)
);

CREATE TABLE JobDepartment (
  dept_ID INT PRIMARY KEY AUTO_INCREMENT,
  emp_ID INT,
  department_name VARCHAR(50),
  job_description VARCHAR(100),
  salary_range VARCHAR(50),
  FOREIGN KEY (emp_ID) REFERENCES Employee(emp_ID)
);

CREATE TABLE Payroll (
  payroll_ID INT PRIMARY KEY AUTO_INCREMENT,
  emp_ID INT,
  salary_ID INT,
  leave_days INT,
  date DATE,
  report VARCHAR(100),
  total_amount DECIMAL(10,2),
  FOREIGN KEY (emp_ID) REFERENCES Employee(emp_ID)
);

CREATE TABLE SalaryBonus (
  bonus_ID INT PRIMARY KEY AUTO_INCREMENT,
  emp_ID INT,
  base_amount DECIMAL(10,2),
  annual_salary DECIMAL(10,2),
  bonus_structure VARCHAR(100),
  FOREIGN KEY (emp_ID) REFERENCES Employee(emp_ID)
);
```

### 3️⃣ Insert Sample Data

```sql
INSERT INTO Employee (name, gender, age, contact, email, password)
VALUES 
('John Doe', 'Male', 29, '9876543210', 'john@example.com', 'pass123'),
('Priya Sharma', 'Female', 32, '8765432109', 'priya@example.com', 'pass456');
```

---

## 💡 Key SQL Queries & Insights

### 🧍 Employee Insights

```sql
SELECT COUNT(DISTINCT emp_ID) AS Total_Employees FROM Employee;
SELECT department_name, COUNT(emp_ID) AS Employee_Count FROM JobDepartment GROUP BY department_name;
SELECT department_name, AVG(base_amount) AS Avg_Salary FROM SalaryBonus GROUP BY department_name;
SELECT name, annual_salary FROM SalaryBonus ORDER BY annual_salary DESC LIMIT 5;
```

**Insight:** Track total employees, salary distribution, and top earners.

---

### 🧑‍💼 Job Role & Department Analysis

```sql
SELECT department_name, COUNT(DISTINCT job_description) AS Job_Roles FROM JobDepartment GROUP BY department_name;
SELECT job_description, MAX(salary_range) AS Max_Salary FROM JobDepartment GROUP BY job_description;
```

**Insight:** Identify salary hierarchy and job role diversity per department.

---

### 🎓 Qualification Analysis

```sql
SELECT COUNT(DISTINCT emp_ID) AS Qualified_Employees FROM Qualification;
SELECT emp_ID, COUNT(qualification_details) AS No_of_Qualifications FROM Qualification GROUP BY emp_ID ORDER BY No_of_Qualifications DESC;
```

**Insight:** Evaluate employee skill depth and qualification trends.

---

### 🏖️ Leave & Absence Patterns

```sql
SELECT YEAR(date) AS Year, SUM(leave_days) AS Total_Leaves FROM Payroll GROUP BY YEAR(date);
SELECT department_name, AVG(leave_days) AS Avg_Leaves FROM Payroll p JOIN JobDepartment j ON p.emp_ID = j.emp_ID GROUP BY department_name;
```

**Insight:** Observe department-wise attendance and workload balance.

---

### 💰 Payroll & Bonus Analysis

```sql
SELECT SUM(total_amount) AS Total_Payroll FROM Payroll;
SELECT department_name, AVG(annual_salary) AS Avg_Bonus FROM SalaryBonus s JOIN JobDepartment j ON s.emp_ID = j.emp_ID GROUP BY department_name;
```

**Insight:** Measure total salary expenditure and reward patterns.

---

## 🧰 Challenges Faced

* Designing and normalizing multi-entity relationships
* Managing cascading updates and deletes
* Writing complex joins for multi-table reports
* Maintaining date consistency across tables
* Preventing duplicate records with unique constraints

---

## ✅ Outcomes

* Fully functional SQL-based HR management system
* Efficient relational schema ensuring integrity and accuracy
* Actionable insights through structured analysis
* Foundation for integration with dashboards or apps

---

## 🚀 Future Enhancements

* Develop a **Flask/React** front-end
* Add **Power BI dashboards** for visualization
* Implement **email automation** for payroll updates
* Deploy database on **AWS RDS or Azure SQL**

---

## 🏷️ Tags

`SQL` `MySQL` `Database` `Employee Management` `Payroll` `HR Analytics` `Data Analysis` `Innomatics` `Relational Database`

---

## 📜 License
This project is for educational and portfolio purposes only.
Unauthorized use or reproduction is not permitted without permission.

---

## 🙌 Acknowledgments

Special thanks to **Innomatics Research Labs** for their mentorship and guidance throughout this project.


---
