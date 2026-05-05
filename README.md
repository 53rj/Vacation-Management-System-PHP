# 🚀 Vacation Management System (PHP)

A web-based application for managing vacation requests, sick leave, and employee data with role-based access control.

---

## 📸 Preview

<!-- Add screenshot here -->
<!-- Example: ![Dashboard](./screenshots/dashboard.png) -->

---

## ✨ Features

- Role-based access control:
  - **Employee:** submit vacation requests and view dashboard  
  - **Department Lead:** approve/reject requests and register sick leave  
  - **Admin:** manage users and maintain core data tables  
- Vacation request system with automatic working-day calculation (weekends excluded via SQL)  
- Approval workflow for vacation requests  
- Sick leave tracking with overlap handling (adjusts vacation balance if necessary)  
- Admin dashboard with full CRUD functionality (personnel, vacation, sickness)  
- Secure authentication using PHP sessions and password hashing (`password_hash`, `password_verify`)  

---

## 🧠 What I Learned

- Building full-stack applications using PHP and MySQL  
- Designing role-based access and permission systems  
- Implementing business logic using SQL (e.g. working-day calculations)  
- Handling edge cases such as overlapping vacation and sick leave  
- Structuring applications into reusable and maintainable components  

---

## 🛠 Tech Stack

- **Backend:** PHP (PDO)  
- **Database:** MySQL / MariaDB  
- **Frontend:** HTML, CSS, JavaScript  

---

## ⚙️ Setup

### 1. Clone repository
```bash
git clone <your-repo-url>
cd urlaubsverwaltung
```

### 2.Create database
```bash
mysql -u root -p -e "CREATE DATABASE urlaubsverwaltung CHARACTER SET utf8mb4;"
```

### 3. Import schema
```bash
mysql -u root -p urlaubsverwaltung < urlaubsverwaltung.sql
```

### 4. Configure database connection

Update credentials in:

f_function.php (main connection via connServer())
register.php
udbv.php

5. Start application

Open in browser:
```
http://localhost/login.php
```

📂 Project Structure
File	Description
login.php	Authentication system
index.php	Dashboard (leave balance, requests overview)
uantrag.php	Submit vacation requests
ugenehmigen.php	Approve/reject requests (department lead)
keintrag.php	Register sick leave
register.php	User registration (admin)
udbv.php	Admin data view (personnel, vacation, sickness tables)
f_function.php	Core logic, session handling, SQL queries
🔐 Security Notes

This project was built for learning purposes.

Before production use, improvements would be required:

Centralized configuration (no hardcoded DB credentials)
CSRF protection
Strict use of prepared statements
Secure password policies


📌 Disclaimer

This project was created as part of a training program and is not intended for production use.

👨‍💻 Authors
Sergiy Stümpel
Marco Wedemeyer
Civan Adam
