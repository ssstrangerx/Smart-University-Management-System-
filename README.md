# SUMS — Smart University Management System

![KRMU Logo](logo.jpg)

## Project Description

SUMS (Smart University Management System) is a web-based platform for K.R. Mangalam University that streamlines academic operations across student, teacher, and admin dashboards. Features include QR-based attendance with anti-cheating rotation, internal assessment management, real-time notice delivery, fee tracking, and grievance handling — all in one unified system.

---

## Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | HTML5, CSS3, JavaScript             |
| Backend   | Python (Flask)                      |
| Database  | MySQL (via MySQL Workbench)         |
| Hosting   | PythonAnywhere / Railway            |

---

## Features

### Student Dashboard
- **Attendance** — View subject-wise and overall attendance percentage
- **Timetable** — Semester-wise class schedule
- **Fees** — Check payment status (paid / partial / unpaid)
- **Notices & Announcements** — View notices sent by teachers and admin
- **Academic Calendar** — University events, holidays, exam dates
- **Mentor-Mentee** — Assigned mentor details and meeting schedule
- **Complaints / Grievance** — File complaints (routed directly to admin)
- **Exam Hub**
  - Admit Card — Download/view admit cards
  - Exam Form — Fill and submit exam forms
  - Report Card — View semester results
- **Scan QR** — Mark attendance by scanning QR code displayed by teacher

### Teacher Dashboard
- **Timetable** — View assigned lecture schedule
- **Mark Attendance**
  - Via QR Code — Generate rotating QR (changes every 3 seconds to prevent cheating)
  - Manually — Mark attendance by selecting class, section, and date
  - Edit Attendance — Modify previously marked records
- **My Subjects** — View all assigned subjects with class/section details
- **Internal Assessment**
  - Midterm (20 marks)
  - Internals (30 marks)
  - Search by roll number or fill for entire section
- **Send Notices** — Select class, semester, section, and broadcast notice
- **Academic Calendar** — View university-wide calendar
- **Grievances / Complaints** — View and respond to student complaints

### Admin Dashboard (Planned)
- **Main Admin** — Full system control across all schools
- **Sub Admin** — School-level management
- View all complaints and grievances
- Manage teacher and student records
- Generate reports

---

## QR Attendance System — How It Works

1. Teacher opens "Mark Attendance" and selects subject + section
2. Server generates a **random token**, stores it with a 3-second expiry
3. QR code with the token is displayed on the teacher's screen
4. QR **refreshes every 3 seconds** — old tokens become permanently invalid
5. Student scans QR while logged in — system verifies both the token and the student's identity
6. If a friend screenshots the QR and sends it, it's already expired by the time they scan

This prevents proxy attendance effectively.

---

## Database Schema (Normalized — ~15 tables)

| Table                | Purpose                                              |
|----------------------|------------------------------------------------------|
| `schools`            | SOET, SOL, SOMC, etc.                                |
| `programs`           | B.Tech CSE, B.Tech AI/ML, etc.                       |
| `sections`           | Year, semester, section (A/B/C/D) per program         |
| `students`           | Student details, roll number, section FK              |
| `teachers`           | Teacher details, employee ID, school FK               |
| `subjects`           | Subject name, code, program, semester                 |
| `teacher_subjects`   | Which teacher teaches which subject to which section  |
| `timetable`          | Day, time slot, subject, teacher, room — per section  |
| `attendance`         | Student, subject, date, status, marked_by (QR/manual) |
| `internal_assessment`| Midterm (20) and internals (30) marks per student     |
| `complaints`         | Filed by student/teacher, routed to admin             |
| `notices`            | Teacher → section-targeted announcements              |
| `admins`             | Main admin and sub-admin accounts                     |
| `qr_tokens`          | Rotating tokens with 3-second expiry                  |
| `fees`               | Semester-wise fee status per student                  |

---

## Project Structure

```
SUMS/
├── logo.jpg                  # University logo (favicon)
├── wallpaper.png             # Background image for forms
├── login.html                # Login page (student + teacher)
├── login_style.css           # Login page styles
├── form.html                 # Student registration form
├── form_style.css            # Student registration styles
├── teacher_form.html         # Teacher registration form
├── teacher_form_style.css    # Teacher registration styles
├── Students.html             # Student dashboard
├── stu_style.css             # Student dashboard styles
├── teacher.html              # Teacher dashboard
├── teacher_style.css         # Teacher dashboard styles
├── connection.py             # (Planned) Flask backend + MySQL connection
├── databases/                # (Planned) SQL schema and seed files
│   └── schema.sql
└── README.md
```

---

## How to Run (Current — Frontend Only)

1. Clone or download the project folder
2. Open `login.html` in any browser
3. Navigate between pages manually (backend not yet connected)

## How to Run (Planned — Full Stack)

```bash
# 1. Install dependencies
pip install flask mysql-connector-python

# 2. Set up MySQL database
mysql -u root -p < databases/schema.sql

# 3. Run Flask server
python connection.py

# 4. Open in browser
# http://127.0.0.1:5000
```

---

## University Hierarchy

```
K.R. Mangalam University
├── SOET (School of Engineering & Technology)
│   ├── B.Tech CSE Core
│   ├── B.Tech AI/ML
│   ├── B.Tech Cybersecurity
│   └── ...
├── SOMC (School of Media & Communication)
├── SOL (School of Law)
├── SOE (School of Education)
├── SOAD (School of Architecture & Design)
└── ...

Each Program → Sections (A, B, C, D) → Years (1-4) → Semesters (1-8)
```

---

## Team

| Role      | Name            |
|-----------|-----------------|
| Developer | Pranav Tripathi |


*K.R. Mangalam University — B.Tech CSE, 2nd Year*

---

## License

This project is developed for academic purposes at K.R. Mangalam University.
