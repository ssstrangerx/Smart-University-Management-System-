# SUMS — Smart University Management System

![KRMU Logo](logo.jpg)

## Project Description

SUMS (Smart University Management System) is a web-based platform for K.R. Mangalam University that streamlines academic operations across student, teacher, and admin dashboards. Features include QR-based attendance with anti-cheating rotation, internal assessment management, real-time notice delivery, fee tracking, and grievance handling — all in one unified system.

---

## Tech Stack

| Layer      | Technology                              |
|------------|-----------------------------------------|
| Frontend   | HTML5, CSS3, JavaScript                 |
| Backend    | Firebase (Authentication + Firestore)   |
| Database   | Cloud Firestore (NoSQL)                 |
| Hosting    | Netlify / Firebase Hosting              |

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
2. Firebase generates a **random token**, stores it in Firestore with a 3-second expiry
3. QR code with the token is displayed on the teacher's screen
4. QR **refreshes every 3 seconds** — old tokens become permanently invalid
5. Student scans QR while logged in — system verifies both the token and the student's identity
6. If a friend screenshots the QR and sends it, it's already expired by the time they scan

This prevents proxy attendance effectively.

---

## Database Structure (Cloud Firestore)

| Collection             | Purpose                                              |
|------------------------|------------------------------------------------------|
| `schools`              | SOET, SOL, SOMC, etc.                                |
| `programs`             | B.Tech CSE, B.Tech AI/ML, etc.                       |
| `sections`             | Year, semester, section (A/B/C/D) per program         |
| `students`             | Student details, roll number, section reference        |
| `teachers`             | Teacher details, employee ID, school reference         |
| `subjects`             | Subject name, code, program, semester                 |
| `teacher_subjects`     | Which teacher teaches which subject to which section  |
| `timetable`            | Day, time slot, subject, teacher, room — per section  |
| `attendance`           | Student, subject, date, status, marked_by (QR/manual) |
| `internal_assessment`  | Midterm (20) and internals (30) marks per student     |
| `complaints`           | Filed by student/teacher, routed to admin             |
| `notices`              | Teacher → section-targeted announcements              |
| `admins`               | Main admin and sub-admin accounts                     |
| `qr_tokens`            | Rotating tokens with 3-second expiry                  |
| `fees`                 | Semester-wise fee status per student                  |

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
├── firebase-config.js        # Firebase initialization and config
└── README.md
```

---

## How to Run

### Prerequisites
- A Firebase project (free tier) with Authentication and Firestore enabled
- Any modern browser

### Setup

1. Clone or download the project
   ```bash
   git clone https://github.com/your-repo/SUMS.git
   ```

2. Create a Firebase project at [console.firebase.google.com](https://console.firebase.google.com)

3. Enable **Email/Password Authentication** in Firebase Console

4. Create a **Cloud Firestore** database

5. Copy your Firebase config into `firebase-config.js`

6. Open `login.html` in a browser, or deploy to Netlify / Firebase Hosting

### Deploy to Netlify

1. Go to [app.netlify.com](https://app.netlify.com)
2. Drag and drop the project folder
3. Your site is live

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

## Developer

| Role                 | Name             |
|----------------------|------------------|
| Full Stack Developer | Pranav Tripathi  |

*K.R. Mangalam University — B.Tech CSE, 2nd Year*

---

## License

This project is developed for academic purposes at K.R. Mangalam University.
