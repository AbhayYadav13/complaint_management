# Group 7 – Student Complaint Management System

An institutional web application through which students can submit grievances, generate unique tracking IDs, review past complaints, update status workflows, and search/track live progress.

---

## 📌 Project Objectives & Scope

The **Student Complaint Management System** facilitates communication between students and college administration. Students can report academic, hostel, library, transport, or lab infrastructure issues, while staff/administrators can manage and resolve them transparently.

---

## 🧱 Module Architecture

The system fulfills all 6 required modules:

| Module | Title | Key Functionality | Page / Script |
|---|---|---|---|
| **Module 1** | **Home Page** | Displays portal overview, grievance redressal policy, core metrics (Total, Pending, In Progress, Resolved), and navigation links. | `index.html` |
| **Module 2** | **Student Details** | Captures student identity: `Name`, `Roll_No`, `Course`, and `Email`. Maps to the `Student` database table. | `submit-complaint.html` |
| **Module 3** | **Submit Complaint** | Form to enter `Subject`, `Category`, and `Description`. Automatically assigns a unique `Complaint_ID` (format `CMP-YYYY-XXXX`). | `submit-complaint.html` |
| **Module 4** | **Complaint Records** | Displays all submitted complaints joined with student details (`Complaint_ID`, Student profile, `Subject`, `Category`, and `Status`). Includes filters & search. | `complaint-records.html` |
| **Module 5** | **Update Complaint Status** | Allows administrative users to transition status between **Pending**, **In Progress**, and **Resolved**, appending official remarks. | `update-status.html` / Modal |
| **Module 6** | **Search Complaint** | Search by unique `Complaint_ID` to display comprehensive complaint details and a visual 3-stage status tracker. | `search-complaint.html` |

---

## 🗄️ Database Architecture

The application strictly aligns with the suggested relational schema:

### 1. `Student` Table
| Column | Data Type | Constraint | Description |
|---|---|---|---|
| `Student_ID` | `INT` | Primary Key, Auto Increment | Internal unique student identifier |
| `Name` | `VARCHAR(100)` | NOT NULL | Full name of the student |
| `Roll_No` | `VARCHAR(50)` | NOT NULL, UNIQUE | University Roll / Registration Number |
| `Course` | `VARCHAR(100)` | NOT NULL | Degree / Program (e.g., B.Tech CSE, MCA, MBA) |
| `Email` | `VARCHAR(120)` | NOT NULL | Student email address |
| `Created_At` | `TIMESTAMP` | DEFAULT CURRENT_TIMESTAMP | Registration timestamp |

### 2. `Complaint` Table
| Column | Data Type | Constraint | Description |
|---|---|---|---|
| `Complaint_ID` | `VARCHAR(30)` | Primary Key | Formatted ID (e.g., `CMP-2026-1001`) |
| `Student_ID` | `INT` | Foreign Key (`Student.Student_ID`) | References the complainant student |
| `Subject` | `VARCHAR(255)` | NOT NULL | Brief grievance title |
| `Category` | `VARCHAR(100)` | NOT NULL | Grievance category |
| `Description` | `TEXT` | NOT NULL | Comprehensive explanation of the issue |
| `Status` | `ENUM` | Default `'Pending'` | Allowed: `'Pending'`, `'In Progress'`, `'Resolved'` |
| `Remarks` | `TEXT` | NULL | Staff action logs and resolution notes |
| `Created_At` | `TIMESTAMP` | DEFAULT CURRENT_TIMESTAMP | Date and time filed |
| `Updated_At` | `TIMESTAMP` | ON UPDATE CURRENT_TIMESTAMP | Date and time of last status update |

---

## 🛠️ Technology Stack

As requested, this project is built using:
- **HTML5**: Semantic, accessible markup.
- **CSS3**: Custom modern responsive styling, cards, status badges, progress steppers, print stylesheets.
- **JavaScript (ES6+)**: Dynamic form handling, client-side validation, filtering, and asynchronous communication.
- **PHP**: RESTful backend with PDO and MySQL integration.
- **No external frameworks, libraries, or npm packages required!**

### 🔄 Dual-Mode Architecture:
1. **Zero-Setup Client Mode**: Open `index.html` directly in any web browser (`file:///...`). It will use browser `localStorage` pre-loaded with realistic sample records.
2. **Full-Stack PHP/MySQL Mode**: Host in XAMPP/WAMP `htdocs/`. The application automatically detects PHP backend connectivity (`php/api.php?action=check`) and executes real SQL queries on MySQL.

---

## 🚀 How to Run the Project

### Option A: Direct Instant Preview (No Server Needed)
1. Navigate to the project folder:
   ```
   student-complaint-management-system/
   ```
2. Double-click **`index.html`** to open it in Chrome, Edge, Firefox, or Safari.
3. All 6 modules (submission, ID generation, records ledger, status updates, and search tracking) will work immediately with local persistence.

---

### Option B: Running with XAMPP / WAMP (PHP + MySQL)
1. Copy the `student-complaint-management-system` folder into your web server's root:
   - For XAMPP on Windows: `C:\xampp\htdocs\student-complaint-management-system`
2. Start **Apache** and **MySQL** services in the XAMPP Control Panel.
3. Import the database schema:
   - **Method 1 (One-click script):** Open `http://localhost/student-complaint-management-system/php/setup_db.php` in your browser.
   - **Method 2 (phpMyAdmin):** Open `http://localhost/phpmyadmin/`, create a database named `student_complaint_db`, and import `php/schema.sql`.
4. Check credentials in `php/db_connect.php` (default is user: `root`, password: empty `""`).
5. Access the portal in your browser:
   ```
   http://localhost/student-complaint-management-system/
   ```
   The top banner indicator will show: `🟢 Backend: PHP & MySQL Connected`.

---

## 📂 File Structure

```
student-complaint-management-system/
│
├── index.html                  # Module 1: Home page & live stats dashboard
├── submit-complaint.html       # Modules 2 & 3: Student Details + Complaint Form
├── complaint-records.html      # Module 4: Records ledger & table filters
├── update-status.html          # Module 5: Dedicated update complaint status interface
├── search-complaint.html       # Module 6: Search & lifecycle progress tracker
├── index.php                   # PHP server router entry point
├── README.md                   # Complete documentation
│
├── css/
│   └── style.css               # Unified responsive stylesheet
│
├── js/
│   ├── data.js                 # Central data abstraction layer (PHP API + LocalStorage fallback)
│   ├── main.js                 # Global UI helpers, toast notifications, status indicator
│   ├── submit.js               # Form validation & unique Complaint ID generator
│   ├── records.js              # Record rendering, search filter, and status update modal
│   ├── update.js               # Dedicated status update logic & complaint picker
│   └── search.js               # Search by ID & visual 3-stage progress bar
│
└── php/
    ├── db_connect.php          # MySQL PDO database connection
    ├── api.php                 # RESTful backend API handling all 6 modules
    ├── schema.sql              # Database creation and sample seed data
    └── setup_db.php            # One-click browser-based database installer
```
