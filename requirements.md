You are a senior full-stack developer helping me finish a university assignment: a "University Research Opportunity Portal". Build the complete project in the order below. Do not skip the planning stages.

## 1. PROBLEM
Research opportunities at my university are shared through emails, WhatsApp groups, and noticeboards, so students miss them and faculty struggle to manage them. I need a multi-page web app where faculty can post, view, update, and manage research opportunities in one place, with a REST API backend, a MySQL database, and a React frontend with client-side routing.

## 2. REQUIREMENTS

### Data fields (each opportunity)
id (auto-increment), title, description, research_area, faculty_name, department, required_skills, positions_available (integer), application_deadline (date), status (Open or Closed)

### REST API (all operations use MySQL, no hard-coded data)
- POST   /api/opportunities       -> create (201)
- GET    /api/opportunities       -> list all (200)
- GET    /api/opportunities/:id   -> get one (200 / 404)
- PUT    /api/opportunities/:id   -> update, including status Open -> Closed (200 / 400 / 404)
- DELETE /api/opportunities/:id   -> delete (200 / 404)
Status codes: 200, 201, 400, 404, 500.

### Frontend: multi-page React app with React Router
Pages and routes:
- /                      Home: short intro plus link to the list
- /opportunities         List page: all opportunities as cards or a table, with status badge, View, Edit, Close, Delete actions
- /opportunities/new     Create page: form with validation
- /opportunities/:id     Details page: full details, with Edit, Close (Open -> Closed), and Delete buttons
- /opportunities/:id/edit  Edit page: same form, pre-filled from the API
- *                      404 "Page not found" page
Shared layout: Navbar (Home, All Opportunities, Add Opportunity) and footer on every page.

Functional requirements:
1. Display all opportunities (fetched from the API)
2. Display complete details of a selected opportunity
3. Create form
4. Update option
5. Change status Open -> Closed
6. Delete with confirmation
7. Success and error messages (Bootstrap alerts or toasts, also after redirects between pages)
8. Basic validation of required form fields (client-side), plus show server 400 errors
Also add loading and "no data" states. All data comes from the API via fetch or axios, through a small api.js service file. Nothing hard-coded.

### Technology
- Backend: Python (Flask) + flask-cors
- Database: MySQL (mysql-connector-python or PyMySQL, parameterized queries only)
- Frontend: React (Vite) + react-router-dom + Bootstrap
- Credentials in .env (never committed). Provide .env.example and .gitignore (also ignore node_modules).

### Deliverables
Backend and frontend source, database/schema.sql (and optional seed.sql), exported Postman or Bruno collection, README.md (with GitHub link placeholder), a 60-second demo video script, and the final ZIP named P24-0000_NAME_CLASS.zip.

## 3. PLAN
Short step-by-step plan with milestones. Each milestone is one meaningful Git commit (e.g. "Add database schema", "Implement create endpoint", "Set up React Router layout", "Add list page"). Give the exact git commands for each commit.

## 4. ARCHITECTURE
Show the folder structure:

research-opportunity-portal/
  backend/ (app.py, db.py, validators.py, requirements.txt, .env.example)
  frontend/
    src/
      components/ (Navbar, Footer, OpportunityCard, OpportunityForm, Alert, ConfirmModal)
      pages/ (Home, OpportunityList, OpportunityDetails, CreateOpportunity, EditOpportunity, NotFound)
      services/api.js
      App.jsx (routes), main.jsx
    package.json, vite.config.js
  database/ (schema.sql, seed.sql)
  postman/ (collection JSON)
  README.md, .gitignore

Explain how React pages, the API, and MySQL communicate, and how CORS or the Vite proxy is configured.

## 5. DATA MODEL
MySQL CREATE TABLE with proper types, NOT NULL, ENUM('Open','Closed') default 'Open', and CHECK (positions_available >= 0).

## 6. SYSTEM DESIGN
- Document each endpoint with request body, example response, and status codes.
- Validation: required fields, non-negative integer positions, valid YYYY-MM-DD deadline, status Open or Closed. Return 400 with {"error": "..."} listing the problems.
- Global error handler returns 500 without leaking internals. GET/PUT/DELETE on a missing ID returns 404.
- Describe the route-to-page map and the data flow for each page (what API call it makes and what happens on success or error).

## 7. IMPLEMENTATION
Write complete, working, commented code for every file, beginner-readable.

## 8. TESTING
Create the Postman or Bruno collection: 3 creates, get all, get one, update, close (Open -> Closed), delete, GET deleted (404), invalid data (400). Give the importable JSON and manual test steps.

## 9. README.md
Overview, features, tech stack, folder structure, prerequisites, setup steps (create MySQL DB, run schema.sql, create .env, pip install, run Flask, npm install, npm run dev), API table, how to import the collection, GitHub link placeholder, and a note that no credentials are committed.

## 10. DEMO VIDEO SCRIPT
60 seconds, in order: backend running, frontend running, create, list, update, close, delete, one validation or 404 error, then API requests and responses in Postman or Bruno.

## RULES
- Original, clean, simple code. No hard-coded data. All CRUD hits MySQL.
- Never include real passwords or API keys.
- At the end, give a checklist matching the submission requirements and the commands to create the ZIP.