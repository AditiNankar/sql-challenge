# 🧠 SQL Challenge — Pewlett Hackard Employee Database

## 📦 Project Overview

Welcome to the fictional HR data system of **Pewlett Hackard**!  
As a newly hired Data Engineer, your mission is to **reconstruct**, **analyze**, and **query** historical employee records from the 1980s and 1990s using SQL.

This project demonstrates your ability to:
- Design an **Entity Relationship Diagram (ERD)**
- Build a **relational database schema**
- Perform **data analysis using complex SQL queries**

---

## 🗂️ Repository Structure
sql-challenge/
├── EmployeeSQL/
│   ├── data/
│   │   ├── departments.csv
│   │   ├── dept_emp.csv
│   │   ├── dept_manager.csv
│   │   ├── employees.csv
│   │   ├── salaries.csv
│   │   └── titles.csv
│   ├── schema.sql              # SQL script for table creation
│   ├── queries.sql             # SQL script for analysis queries
│   ├── erd.png                 # Entity Relationship Diagram
│   └── README.md
---

## 🛠️ Tools & Technologies

- PostgreSQL  
- pgAdmin 4  
- SQL (DDL, DML, JOINs, WHERE, GROUP BY)  
- QuickDBD (for ERD design)  

---

## 🧩 Part 1: Data Modeling

### ✅ Task
Examine all CSV files and design an ERD to visualize table relationships and data flow.

### 🧱 Tables Designed
- `departments`: department_id (PK), department_name  
- `employees`: emp_no (PK), birth_date, first_name, last_name, sex, hire_date  
- `dept_emp`: emp_no (PK, FK), dept_no (PK, FK), from_date, to_date  
- `dept_manager`: dept_no (PK, FK), emp_no (PK, FK), from_date, to_date  
- `salaries`: emp_no (PK, FK), salary, from_date, to_date  
- `titles`: emp_no (PK, FK), title, from_date, to_date  

---

## 🛠️ Part 2: Data Engineering

### ✅ Steps
1. Created the database `employee_db` in PostgreSQL.
2. Defined table schemas with:
   - Primary and foreign key constraints
   - Appropriate data types (e.g., `VARCHAR`, `DATE`, `INTEGER`)
   - `NOT NULL` constraints where needed
3. Created tables in `schema.sql` in dependency order.
4. Imported CSVs using pgAdmin `Import/Export` tool.

---

## 🔍 Part 3: Data Analysis

Using SQL queries to answer important business questions in `queries.sql`.

### 🧪 Key Queries
- 👩‍💼 **Employee Overview**  
  `SELECT emp_no, last_name, first_name, sex, salary FROM employees JOIN salaries USING(emp_no);`

- 📅 **Employees Hired in 1986**  
  `SELECT first_name, last_name, hire_date FROM employees WHERE EXTRACT(YEAR FROM hire_date) = 1986;`

- 🧑‍💼 **Department Managers**  
  `SELECT d.dept_no, d.dept_name, e.emp_no, e.last_name, e.first_name FROM dept_manager dm JOIN departments d ON dm.dept_no = d.dept_no JOIN employees e ON dm.emp_no = e.emp_no;`

- 🏢 **Department Assignments**  
  `SELECT de.dept_no, e.emp_no, e.last_name, e.first_name, d.dept_name FROM dept_emp de JOIN employees e ON de.emp_no = e.emp_no JOIN departments d ON de.dept_no = d.dept_no;`

- 🦸 **Hercules Employees**  
  `SELECT first_name, last_name, sex FROM employees WHERE first_name = 'Hercules' AND last_name LIKE 'B%';`

- 🏷️ **Sales Employees**  
  `SELECT e.emp_no, e.last_name, e.first_name FROM employees e JOIN dept_emp de ON e.emp_no = de.emp_no JOIN departments d ON de.dept_no = d.dept_no WHERE d.dept_name = 'Sales';`

- 🧪 **Sales & Development Employees**  
  `SELECT e.emp_no, e.last_name, e.first_name, d.dept_name FROM employees e JOIN dept_emp de ON e.emp_no = de.emp_no JOIN departments d ON de.dept_no = d.dept_no WHERE d.dept_name IN ('Sales', 'Development');`

- 📊 **Most Common Last Names**  
  `SELECT last_name, COUNT(*) AS frequency FROM employees GROUP BY last_name ORDER BY frequency DESC;`

---

## 📊 Sample Output (Abbreviated)

| emp_no | last_name | first_name | sex | salary |
|--------|-----------|------------|-----|--------|
| 10001  | Facello   | Georgi     | M   | 60117  |
| 10002  | Simmel    | Bezalel    | F   | 65828  |

---

## 📌 Key Learnings

- Solidified understanding of **relational databases**
- Gained practice in **designing schemas** from raw data
- Enhanced SQL querying techniques using **joins, filters, and aggregates**
- Applied **data normalization principles** to improve structure and maintain referential integrity

---

## 🚀 Getting Started

1. Clone the repo:
```bash
git clone https://github.com/yourusername/sql-challenge.git
cd sql-challenge/EmployeeSQL
2.	Open pgAdmin, create a new DB: employee_db
3.	Run schema.sql to create tables
4.	Import CSV data into each table using the Import/Export tool in pgAdmin
5.	Run queries.sql to generate insights

⸻

👩‍💻 Author

Aditi Nankar
Junior Data Engineer | SQL Enthusiast | Schema Designer

📜 License

This project is for academic and educational purposes only. © 2025
