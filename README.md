# Student Information System Database (`sms_db`)

This repository contains the SQL database schema and initial dummy data for a **Student Information System (SIS)**. It is designed to support the backend operations of an educational institution, managing students, teachers, courses, results, and administrative tasks.

## 🗄️ Database Overview

*   **Database Name:** `sms_db`
*   **DBMS:** MySQL / MariaDB (Exported via phpMyAdmin)
*   **Collation:** `utf8mb4_general_ci`

## 🚀 Key Features Supported by the Schema

Based on the database structure, this system is equipped to handle:
*   **User Management:** Separate tables and roles for `admin`, `teachers`, and `students`.
*   **Academic Structure:** Management of `department`s, `courses`, and `sem_course_list` (semester planning).
*   **Enrollment & Grading:** Tracking student course registrations (`register_std_course`), academic `result`s, and `gpa`.
*   **Financials:** Managing student `fee` structures (tuition, lab, library, etc.).
*   **Communication:** Internal `message` system and student `feedback`.
*   **System Configuration:** Global `setting` table for school name, current semester, and academic year.

## 📋 Schema Summary (Key Tables)

| Table Name | Description |
| :--- | :--- |
| `admin` | Stores administrator credentials and profiles. |
| `students` | Contains student demographics, contact info, and academic intake details. |
| `teachers` | Contains teacher profiles, qualifications, and employee details. |
| `courses` | Catalog of all available courses, credits, and types (Theory/Lab/Project). |
| `department` | Lists academic departments and their respective heads. |
| `result` / `gpa` | Stores individual course grades and calculated semester GPAs. |
| `fee` | Tracks fee structures based on semester, department, and student. |

## 🛠️ Installation & Setup

To use this database in your local development environment (using XAMPP, WAMP, or any MySQL/MariaDB server):

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git)
