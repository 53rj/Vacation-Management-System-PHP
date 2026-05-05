# Vacation Management System (PHP)

A small **PHP** web application for tracking annual leave, leave requests, and sick-leave records. The user interface is **German**; this document is in English for broader readability.

The app was built as a class project (see `meta.html` for authors: Sergiy Stümpel, Marco Wedemeyer, Civan Adam) and targets a fictional “IT-Solutions GmbH” vacation workflow.

## Features

- **Authentication** with PHP sessions; passwords stored with `password_hash()` / verified with `password_verify()` (`login.php`).
- **Role-based access** (stored in `personal.status`):
  - **Angestellter** (employee): dashboard, submit vacation requests.
  - **Abteilungsleiter** (department lead): same as employee, plus approve/reject pending requests and register sick leave (AU) for staff by personnel ID.
  - **Admin**: same as employee, plus register new users and browse/edit core tables (personnel, vacation requests, sick leave).
- **Vacation requests** (`uantrag.php`): date range → working days counted (weekends excluded via SQL in `f_function.php`).
- **Leave balance** (`resturlaub`): updated when requests are approved; sick-leave logic can adjust balances when periods overlap approved vacation.
- **Admin data views** (`udbv.php`): switch between personnel, vacation, and sickness tables (`?table=1|2|3`) with linked edit/update/delete flows.

## Requirements

- **PHP** 7.4+ (8.x used in original export) with extensions: `pdo_mysql`, `session`, `json` (typical PHP–MySQL stack).
- **MySQL** or **MariaDB** (dump created with MariaDB 10.4 / phpMyAdmin).

No Composer or Node build step; assets are plain HTML, CSS, and a small `registration.js`.

## Installation

1. **Clone** this repository and point your web server document root (or a virtual host) at the project directory.

2. **Create the database** and import the schema plus sample data:

   ```bash
   mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS urlaubsverwaltung CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;"
   mysql -u root -p urlaubsverwaltung < urlaubsverwaltung.sql
   ```

3. **Configure database credentials** in code. The default connection uses `localhost`, database `urlaubsverwaltung`, user `root`, and an **empty** password (`connServer()` in `f_function.php`). The same DSN pattern appears in other files (e.g. `register.php`, `udbv.php`); adjust **every** occurrence if you change user, password, or host.

4. Open **`login.php`** in the browser (not `index.php` without a session—you will be redirected to login).

### Sample data

`urlaubsverwaltung.sql` contains example users with **bcrypt** hashes. To log in you need the plaintext passwords used when those accounts were created, or create a new admin user by importing/updating the database accordingly.

## Project layout (main entry points)

| File | Purpose |
|------|---------|
| `login.php` / `login.html` | Login |
| `logout.php` | End session |
| `index.php` | Dashboard: remaining leave, approved/pending/rejected requests |
| `uantrag.php` | Submit vacation request |
| `ugenehmigen.php` | Department lead: pending requests, approve/deny |
| `keintrag.php` | Department lead: sick-leave entry for a given `pid` |
| `register.php` / `register.html` | Admin: register users (`registration.js` confirmation step) |
| `udbv.php` | Admin: table overview + links to `personaltabelle.php`, `urlaubstabelle.php`, `krankheitstabelle.php` |
| `f_function.php` | PDO connection, session guard (`checkStatus`), core business SQL |
| `*_header.html` | Role-specific navigation shell |
| `style.css` | Styling |

Edit/update/delete scripts (`edit_*.php`, `update_*.php`, `delete_eintrag.php`) support admin maintenance of records.

## Security note (production)

This repository is suitable for **learning or internal demos**. Before any production use you should at least: use strong DB credentials, HTTPS, centralized configuration, parameterized queries everywhere, CSRF protection on forms, and a proper password policy. Some legacy helpers in `f_function.php` (e.g. unused `login()` posting raw values into SQL) must not be used as a security reference; the actual login path is `login.php`, which uses prepared statements and `password_verify`.

## License

No license file is included in the repository. If you reuse the code, clarify ownership and terms with the original authors.
