<h1 align="center">🧠 Full Stack RBAC Platform</h1>

<p align="center">
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React">
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js">
  <img src="https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white" alt="Express.js">
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB">
  <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white" alt="JWT">
  <img src="https://img.shields.io/badge/TailwindCSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="TailwindCSS">
</p>

<p align="center">
  A complete <strong>Role-Based Access Control (RBAC)</strong> web application built with the <strong>MERN Stack</strong> — MongoDB, Express, React, and Node.js.
  <br />
  This project showcases secure authentication, authorization, CRUD operations, and audit logging — all in a sleek, responsive, and modern UI.
</p>

---

## 📚 Table of Contents

* [🚀 Features](#-features)
* [🏗️ Tech Stack](#%EF%B8%8F-tech-stack)
* [⚙️ Installation & Setup](#%EF%B8%8F-installation--setup)
* [🧩 API Overview](#-api-overview)
* [🧠 RBAC Permission Model](#-rbac-permission-model)
* [🌱 Database Seeding](#-database-seeding)
* [🧭 Frontend Routes](#-frontend-routes)
* [🧰 Developer Notes](#-developer-notes)
* [🧱 Build for Production](#-build-for-production)
* [🧾 License](#-license)
* [👤 Author](#-author)

---

## 🚀 Features

### 🔐 Authentication & Authorization

* Secure JWT-based authentication with refresh tokens.
* Role-Based Access Control (RBAC) for fine-grained permissions.
* Persistent sessions with token refresh flow.
* Rate limiting to prevent brute-force attacks.

### 👥 User Roles

| Role       | Permissions Summary                              |
| ---------- | ------------------------------------------------ |
| **Admin**  | Full access: manage users, posts, and audit logs |
| **Editor** | Create, read, edit, and delete own posts         |
| **Viewer** | Read-only content access                         |

### 🧩 Backend API (Node.js + Express)

* RESTful endpoints with modular architecture.
* Mongoose models for `User`, `Content`, and `AuditLog`.
* Secure middleware for authentication & authorization.
* Audit logging for key actions like login, registration, and role updates.

### 🎨 Frontend (React)

* React Router v6 for smooth routing.
* TailwindCSS + custom dark aurora-inspired theme.
* Axios hooks for secure API communication.
* Responsive, mobile-friendly layout.

---

## 🏗️ Tech Stack

| Layer          | Technology                                |
| -------------- | ----------------------------------------- |
| **Frontend**   | React, React Router, Axios, TailwindCSS   |
| **Backend**    | Node.js, Express.js, JWT, Mongoose        |
| **Database**   | MongoDB                                   |
| **Security**   | bcrypt, cookie-parser, express-rate-limit |
| **Logging**    | Morgan                                    |
| **Validation** | express-validator                         |

---

## ⚙️ Installation & Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yatinsingh825/fsd_project.git
cd fsd_project
```

### 2️⃣ Setup Backend

```bash
cd backend
npm install
```

Create a `.env` file with the following:

```env
PORT=5001
MONGO_URI=mongodb://localhost:27017/rbac-db
ACCESS_TOKEN_SECRET=your-access-token-secret-key
REFRESH_TOKEN_SECRET=your-refresh-token-secret-key
```

Run the backend server:

```bash
npm start
```

Backend runs at: **[http://localhost:5001](http://localhost:5001)**

### 3️⃣ Setup Frontend

```bash
cd ../frontend
npm install
npm start
```

Frontend runs at: **[http://localhost:3000](http://localhost:3000)**

---

## 🧩 API Overview

### 🔑 Authentication Routes

| Method | Endpoint             | Description              |
| ------ | -------------------- | ------------------------ |
| POST   | `/api/auth/register` | Register new user        |
| POST   | `/api/auth/login`    | Login user               |
| POST   | `/api/auth/refresh`  | Refresh JWT token        |
| POST   | `/api/auth/logout`   | Logout and clear cookies |

### 📝 Content Routes

| Method | Endpoint           | Description     | Role Access         |
| ------ | ------------------ | --------------- | ------------------- |
| GET    | `/api/content`     | Get all posts   | All logged-in       |
| GET    | `/api/content/:id` | Get single post | All logged-in       |
| POST   | `/api/content`     | Create post     | Editor, Admin       |
| PUT    | `/api/content/:id` | Edit post       | Editor (own), Admin |
| DELETE | `/api/content/:id` | Delete post     | Editor (own), Admin |

### 👤 Admin Routes

| Method | Endpoint              | Description      | Role Access |
| ------ | --------------------- | ---------------- | ----------- |
| GET    | `/api/users`          | Get all users    | Admin       |
| PUT    | `/api/users/:id/role` | Update user role | Admin       |
| GET    | `/api/audit-logs`     | View audit logs  | Admin       |

---

## 🧠 RBAC Permission Model

| Resource      | Admin                               | Editor                                  | Viewer |
| ------------- | ----------------------------------- | --------------------------------------- | ------ |
| **Content**   | Create / Read / Update / Delete All | Create / Read / Update Own / Delete Own | Read   |
| **Users**     | Read / Update / Delete              | —                                       | —      |
| **Audit Log** | Read                                | —                                       | —      |

---

## 🌱 Database Seeding

Automatically seeds initial users and posts:

| Username | Password       | Role   |
| -------- | -------------- | ------ |
| admin    | adminpassword  | Admin  |
| editor   | editorpassword | Editor |
| viewer   | viewerpassword | Viewer |

---

## 🧭 Frontend Routes

| Path            | Access              | Description              |
| --------------- | ------------------- | ------------------------ |
| `/`             | Logged-in           | Home / Content feed      |
| `/login`        | Public              | Login page               |
| `/register`     | Public              | Register page            |
| `/create`       | Editor, Admin       | Create post              |
| `/edit/:id`     | Editor (own), Admin | Edit post                |
| `/admin`        | Admin               | Admin dashboard          |
| `/admin/users`  | Admin               | Manage user roles        |
| `/admin/audit`  | Admin               | View audit logs          |
| `/unauthorized` | All                 | Unauthorized access page |

---

## 🧰 Developer Notes

### 🔄 Auth Flow

* Axios interceptors handle expired tokens and auto-refresh.
* Backend enforces short-lived access tokens (15 min) and long refresh tokens (7 days).

### 🔒 Security

* Passwords hashed via **bcrypt**.
* Rate limiting on authentication endpoints.
* Cookies HttpOnly for protection against XSS.

### 🧾 Audit Logging

* Tracks user actions: login, registration, role changes.
* Admin dashboard displays latest logs.

---

## 🧱 Build for Production

**Frontend:**

```bash
cd frontend
npm run build
```

**Backend:**

```bash
node server.js
```

Deploy frontend via **Vercel**, **Netlify**, or **Nginx**, ensuring backend URL is properly configured in `.env`.

---

## 📸 UI Highlights

* 🌌 Aurora-inspired glassmorphism design.
* 💻 Admin dashboard with live data.
* 🔒 Smart route protection.
* 🧑‍💼 Intuitive login/register forms.

---



