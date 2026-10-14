# 🎓 University Research Opportunity Portal

A modern, full-stack web application designed for university faculty and students to publish, discover, apply for, and manage academic research projects in one centralized platform.

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/YOUR_GITHUB_USERNAME/research-opportunity-portal)
[![React](https://img.shields.io/badge/Frontend-React_18_%2B_Vite-61dafb?logo=react)](https://reactjs.org/)
[![Flask](https://img.shields.io/badge/Backend-Flask_3-000000?logo=flask)](https://flask.palletsprojects.com/)
[![MySQL](https://img.shields.io/badge/Database-MySQL_8.0-4479a1?logo=mysql)](https://www.mysql.com/)

---

## 📌 1. Project Overview

At universities, research opportunities are typically broadcast informally across fragmented email listservs, messaging groups, and physical bulletin boards. As a result, eager students miss critical deadlines and faculty struggle to track positions and filter applicants.

The **University Research Opportunity Portal** solves this problem by providing:
- A responsive, multi-page **React (Vite)** interface with client-side routing.
- A robust **Python Flask REST API** implementing full CRUD operations.
- A relational **MySQL database** with constraints and parameterized queries preventing SQL injection.

> **Security Note:** Real database credentials and sensitive secrets are **never committed** to source control. Configuration is strictly managed via `.env` files following the 12-factor application methodology.

---

## 🚀 2. Features

- **Multi-Page Single Page App (SPA)**: Powered by React Router v6 with smooth client-side page transitions.
- **Dynamic Research Feed**: Live listings loaded via `api.js` with instant client-side keyword search and status filtering (All, Open, Closed).
- **Opportunity Details View**: Full overview of project descriptions, prerequisite competencies, faculty contact, and position counts.
- **Faculty Management Form**: Create and update research vacancies with rigorous client-side and server-side validation.
- **Lifecycle Transition (Open → Closed)**: Instantly mark vacancies as closed when positions are filled.
- **Destructive Action Safety**: Custom Bootstrap confirmation modal prevents accidental project deletion.
- **Flash Notifications**: Contextual alerts for creates, updates, and deletions across page redirects.
- **Graceful Error Handling**: Custom 404 page for missing records and global 500 handler that protects internal stack traces.

---

## 🛠️ 3. Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite 5, React Router DOM v6, Bootstrap 5.3, Bootstrap Icons |
| **Backend** | Python 3.10+, Flask 3.0, Flask-CORS, PyMySQL, Cryptography, Python-Dotenv |
| **Database** | MySQL 8.0+ / MariaDB (InnoDB, UTF8mb4) |
| **Testing** | Postman / Bruno API Test Collection |

---

## 📂 4. Project Directory Structure

```text
research-opportunity-portal/
├── backend/
│   ├── .env.example          # Environment variables template
│   ├── app.py                # Flask REST API endpoints & global error handlers
│   ├── db.py                 # MySQL connection manager & DictCursor pooling
│   ├── requirements.txt      # Python dependencies
│   └── validators.py         # Request payload validators & rule checks
├── frontend/
│   ├── public/               # Static assets & favicon
│   ├── src/
│   │   ├── components/
│   │   │   ├── Alert.jsx             # Dismissible notification banners
│   │   │   ├── ConfirmModal.jsx      # Reusable confirmation dialogs
│   │   │   ├── Footer.jsx            # Portal footer layout
│   │   │   ├── Navbar.jsx            # Sticky responsive navigation bar
│   │   │   ├── OpportunityCard.jsx   # Grid card with actions & status badges
│   │   │   └── OpportunityForm.jsx   # Create/Edit form with validation
│   │   ├── pages/
│   │   │   ├── CreateOpportunity.jsx # Creation page (/opportunities/new)
│   │   │   ├── EditOpportunity.jsx   # Update page (/opportunities/:id/edit)
│   │   │   ├── Home.jsx              # Hero landing page (/)
│   │   │   ├── NotFound.jsx          # 404 error page (*)
│   │   │   ├── OpportunityDetails.jsx# Detailed opportunity page (/opportunities/:id)
│   │   │   └── OpportunityList.jsx   # Catalog listing (/opportunities)
│   │   ├── services/
│   │   │   └── api.js        # Centralized fetch service layer
│   │   ├── App.jsx           # Route definitions & app layout
│   │   ├── index.css         # Custom typography & design system
│   │   └── main.jsx          # React DOM entry point
│   ├── index.html            # HTML shell with Bootstrap & Google Fonts
│   ├── package.json          # Node dependencies & Vite scripts
│   └── vite.config.js        # Vite config with API reverse proxy
├── database/
│   ├── schema.sql            # Table definitions with CHECK & ENUM constraints
│   └── seed.sql              # Initial realistic seed datasets
├── docs/
│   └── demo_script.md        # 60-second video presentation script
├── postman/
│   └── Research_Opportunity_Portal.postman_collection.json # API collection
├── .gitignore                # Git exclusions (node_modules, venv, .env)
└── README.md                 # Project documentation
```

---

## 📋 5. Prerequisites

Before running the application, make sure you have installed:
1. **Python 3.10+** (`python --version`)
2. **Node.js 18+ & npm** (`node -v` and `npm -v`)
3. **MySQL Server 8.0+** or **XAMPP / MariaDB**

---

## ⚙️ 6. Step-by-Step Setup Guide

### Step 1: Database Setup
1. Launch your MySQL command line client or phpMyAdmin:
   ```bash
   mysql -u root -p
   ```
2. Execute the schema script to create the database, tables, and constraints:
   ```sql
   SOURCE database/schema.sql;
   ```
3. *(Optional)* Seed initial sample records:
   ```sql
   SOURCE database/seed.sql;
   ```

---

### Step 2: Backend Configuration & Launch
1. Open a terminal and navigate to the `backend` folder:
   ```bash
   cd backend
   ```
2. Create and activate a Python virtual environment:
   ```bash
   # Windows PowerShell:
   python -m venv venv
   .\venv\Scripts\Activate.ps1

   # macOS / Linux:
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```
4. Configure your `.env` file from the provided template:
   ```bash
   # Windows:
   copy .env.example .env

   # macOS / Linux:
   cp .env.example .env
   ```
5. Open `.env` in a text editor and enter your local MySQL credentials:
   ```env
   DB_HOST=localhost
   DB_PORT=3306
   DB_USER=root
   DB_PASSWORD=your_actual_mysql_password
   DB_NAME=research_portal
   PORT=5000
   ```
6. Start the Flask REST API server:
   ```bash
   python app.py
   ```
   *The backend will be running at `http://127.0.0.1:5000`.*

---

### Step 3: Frontend Configuration & Launch
1. Open a **second terminal** and navigate to the `frontend` directory:
   ```bash
   cd frontend
   ```
2. Install frontend dependencies:
   ```bash
   npm install
   ```
3. Start the Vite development server:
   ```bash
   npm run dev
   ```
4. Open your browser and navigate to:
   ```
   http://localhost:3000
   ```

---

## 📡 7. REST API Documentation

| Method | Endpoint | Description | Request Body | Status Codes |
|---|---|---|---|---|
| **GET** | `/api/opportunities` | Retrieve all opportunities | None | `200` |
| **GET** | `/api/opportunities/:id` | Retrieve single opportunity | None | `200`, `404` |
| **POST** | `/api/opportunities` | Create a new opportunity | JSON Object (all required fields) | `201`, `400`, `500` |
| **PUT** | `/api/opportunities/:id` | Update opportunity fields or status | JSON Object (partial or full fields) | `200`, `400`, `404`, `500` |
| **DELETE** | `/api/opportunities/:id` | Remove opportunity | None | `200`, `404`, `500` |
| **GET** | `/api/health` | Service and MySQL health status | None | `200`, `500` |

### Sample JSON Payload for POST `/api/opportunities`:
```json
{
  "title": "Autonomous UAV Swarm Protocol Optimization",
  "description": "Simulating peer-to-peer localization algorithms for drone networks in GPS-compromised flight zones.",
  "research_area": "Robotics & Wireless Networks",
  "faculty_name": "Prof. Tariq Mahmood",
  "department": "Electrical Engineering",
  "required_skills": "ROS 2, C++, Python, Mesh Networking",
  "positions_available": 2,
  "application_deadline": "2026-11-30",
  "status": "Open"
}
```

---

## 🧪 8. API Testing with Postman or Bruno

An exported Postman Collection v2.1.0 is located at:
`postman/Research_Opportunity_Portal.postman_collection.json`

### Import Instructions:
1. Open **Postman** (or **Bruno**).
2. Click **Import** in the top left corner.
3. Select the file `postman/Research_Opportunity_Portal.postman_collection.json`.
4. Ensure the collection variable `baseUrl` is set to `http://localhost:5000`.
5. Execute requests 1 through 11 in sequential order:
   - 3 consecutive `POST` creates
   - `GET` all opportunities
   - `GET` single opportunity
   - `PUT` update opportunity
   - `PUT` close status (Open → Closed)
   - `DELETE` opportunity
   - `GET` deleted opportunity (verifies `404`)
   - `POST` invalid payload (verifies `400`)
   - `PUT` negative positions (verifies `400`)

---

## 🎥 9. Demo Video Script

A full 60-second walkthrough script is available in:
[`docs/demo_script.md`](./docs/demo_script.md)

---

## 📄 10. License & Academic Integrity

This project is submitted for university coursework. All code is original, commented, and complies with university academic policies.
