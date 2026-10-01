# ProjectMS — Smart Project Management System

A full-stack, role-based project management web application. Admins, Project Managers and Employees each get their own dashboard to manage users, projects, milestones and tasks, with a built-in AI Insight module that analyses uploaded project documents.

## Features

- **Role-based access** — Admin, Project Manager and Employee roles secured with JWT authentication
- **User management** — Admins create and manage Project Managers and Employees within their department
- **Projects and teams** — Create projects, assign team members, track project statistics
- **Milestone planner** — Plan and track milestones for each project
- **Task management** — Assign tasks, update progress and view task history
- **Dashboards** — Separate dashboards with charts for Admin, Manager and Employee
- **AI Insight** — Upload PDF/Excel documents and get insights using a pure-Java TF-IDF engine (no external API needed)

## Tech Stack

| Layer    | Technologies                                                         |
|----------|----------------------------------------------------------------------|
| Backend  | Java 21, Spring Boot 3.3, Spring Security (JWT), Spring Data JPA, Hibernate |
| Database | SQLite                                                               |
| Frontend | React 18, React Router, Axios, Recharts, React Hot Toast, Lucide Icons |
| AI/Docs  | TF-IDF (custom Java), Apache PDFBox, Apache POI                      |

## Project Structure

```
project-management/
├── backend/                  # Spring Boot REST API
│   └── src/main/java/com/projectms/
│       ├── config/           # Security config, data seeding
│       ├── controller/       # REST controllers
│       ├── dto/              # Request/response objects
│       ├── entity/           # JPA entities
│       ├── ml/               # AI Insight engine
│       ├── repository/       # Spring Data repositories
│       ├── security/         # JWT filter and utilities
│       └── service/          # Business logic
├── frontend/                 # React application
│   └── src/
│       ├── api/              # Axios API calls
│       ├── components/       # Shared components (Sidebar, AI Insight page)
│       ├── context/          # Auth context
│       └── pages/            # admin / manager / employee pages
├── reset-database.sh         # Reset DB (Linux/Mac)
└── reset-database.bat        # Reset DB (Windows)
```

## Prerequisites

- Java 21 (JDK)
- Maven 3.8+
- Node.js 18+ and npm

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/project-management.git
cd project-management
```

### 2. Run the backend

```bash
cd backend
mvn spring-boot:run
```

The API runs at **http://localhost:8080**.

### 3. Run the frontend

Open a new terminal:

```bash
cd frontend
npm install
npm start
```

The app opens at **http://localhost:3000**.

## Default Login Credentials

Admin accounts are seeded automatically on first run:

| Department     | Username    | Password  | Role  |
|----------------|-------------|-----------|-------|
| HR             | admin_hr    | Admin@123 | Admin |
| Project Dev    | admin_pd    | Admin@123 | Admin |
| Administration | admin_adm   | Admin@123 | Admin |
| Cybersecurity  | admin_cs    | Admin@123 | Admin |

Each Admin can create Project Managers and Employees within their department.

> These are demo credentials. Change them before any real deployment.

## Configuration

Settings are in `backend/src/main/resources/application.properties`:

| Property                  | Description                          | Default                   |
|---------------------------|--------------------------------------|---------------------------|
| `server.port`             | Backend port                         | `8080`                    |
| `spring.datasource.url`   | SQLite database file                 | `jdbc:sqlite:./projectms.db` |
| `app.jwt.secret`          | JWT signing key — use your own value | —                         |
| `app.jwt.expiration`      | Token lifetime (ms)                  | `86400000` (24 hours)     |
| `app.cors.allowed-origins`| Allowed frontend origin              | `http://localhost:3000`   |

> `spring.jpa.hibernate.ddl-auto` is set to `create-drop`, so data is wiped on every restart. Change it to `update` if you want data to persist.

## Resetting the Database

If login fails or the schema gets out of sync, delete `backend/projectms.db` and restart the backend, or run:

```bash
./reset-database.sh        # Linux / Mac
reset-database.bat         # Windows
```

## API Overview

| Endpoint prefix      | Purpose                                  |
|----------------------|------------------------------------------|
| `/api/auth`          | Login and current user                   |
| `/api/admin`         | User management and admin statistics     |
| `/api/projects`      | Projects, project stats and team members |
| `/api/milestones`    | Milestones per project                   |
| `/api/tasks`         | Tasks, task updates and personal stats   |
| `/api/ai-insight`    | Document analysis                        |

## Author

**Malini**
B.Tech Information Technology — St. Joseph College of Engineering

## License

This project is for educational purposes.
