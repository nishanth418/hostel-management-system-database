# Hostel Management System

Welcome to the **Hostel Management Combined** repository. This monorepo houses **two completely independent, production-ready editions** of the Hostel Management System, each powered by a different database engine and data model.

---

## 📁 Repository Structure

```text
hostel-management-system/
│
├── .gitignore                     # Monorepo root gitignore rules
├── README.md                      # Monorepo architecture & navigation guide
│
├── hostel-management-mysql/       # PROJECT 1: Aiven Cloud MySQL Edition
│   ├── .env.example               # Environment variables template
│   ├── .gitignore                 # Project-specific gitignore
│   ├── README.md                  # MySQL project documentation
│   ├── backend/                   # Node.js + Express backend (REST API)
│   │   ├── routes/                # 16 domain routes (Students, Rooms, Mess, etc.)
│   │   ├── database.js            # Unified database query dispatcher
│   │   ├── db-mysql.js            # Aiven MySQL pool & connection management
│   │   ├── package.json           # Backend dependencies (mysql2, better-sqlite3)
│   │   └── server.js              # Express entrypoint
│   ├── database/                  # SQL schema definitions & seed files
│   │   ├── schema.sql             # Relational SQL schema
│   │   ├── schema_mysql.sql       # MySQL-tailored schema
│   │   └── seed.sql               # Seed data
│   └── frontend/                  # React + Vite frontend SPA
│       ├── package.json           # Frontend dependencies (React, Three.js, Lucide)
│       ├── vercel.json            # Vercel SPA rewrite configuration
│       ├── vite.config.js         # Vite configuration & dev proxy
│       └── src/                   # React components, pages & 3D canvas
│
└── hostel-management-neo4j/       # PROJECT 2: Neo4j AuraDB Edition
    ├── .env.example               # Environment variables template
    ├── .gitignore                 # Project-specific gitignore
    ├── GRAPH_MODEL.md             # Graph data model & Cypher documentation
    ├── README.md                  # Neo4j project documentation
    ├── backend/                   # Node.js + Express backend (Cypher REST API)
    │   ├── routes/                # 16 domain routes executing Cypher queries
    │   ├── database.js            # Unified database query dispatcher
    │   ├── db-neo4j.js            # Neo4j driver connection management
    │   ├── init-neo4j.js          # Neo4j constraints & schema initializer
    │   ├── package.json           # Backend dependencies (neo4j-driver)
    │   └── server.js              # Express entrypoint
    ├── database/                  # Cypher graph schema & seed files
    │   ├── schema.cypher          # Neo4j node labels, constraints, and relationships
    │   └── seed.cypher            # Cypher graph seed data
    └── frontend/                  # React + Vite frontend SPA (Graph-tailored UI)
        ├── package.json           # Frontend dependencies (React, Three.js, Lucide)
        ├── vercel.json            # Vercel SPA rewrite configuration
        ├── vite.config.js         # Vite configuration & dev proxy
        └── src/                   # React components, pages & 3D canvas
```

---

## 🚀 Projects Overview

| Feature | Project 1: `hostel-management-mysql` | Project 2: `hostel-management-neo4j` |
|---|---|---|
| **Database** | Aiven Cloud MySQL (Relational) | Neo4j AuraDB (Property Graph) |
| **Driver / Client** | `mysql2/promise` (+ SQLite local fallback) | `neo4j-driver` (Bolt + SSL) |
| **Query Language** | SQL (Relational joins & transactions) | Cypher (`MATCH`, `MERGE`, graph traversals) |
| **Backend Port** | `5000` (default) | `5000` (default) |
| **Frontend Port** | `3000` (Vite dev server) | `3000` (Vite dev server) |
| **Backend Scripts** | `npm start`, `npm run init-db`, `npm run verify-db` | `npm start`, `npm run init-db`, `npm run verify-db`, `npm run test-connection` |
| **Status** | Independent Production Service | Independent Production Service |

Both projects maintain their own dependencies, configuration files, and deployment targets. No application code, dependencies, or database structures are shared between the two projects.

---

## 🛠️ Local Development Guide

### 1. Running Project 1 (`hostel-management-mysql`)

```bash
# Navigate to backend and install dependencies
cd hostel-management-mysql/backend
npm install

# Configure environment variables
cp ../.env.example .env
# Edit .env with your Aiven Cloud MySQL credentials:
# DATABASE_URL=mysql://avnadmin:YOUR_PASSWORD@YOUR_HOST:PORT/defaultdb?ssl-mode=REQUIRED

# Start the backend server
npm start
```

In a separate terminal:
```bash
# Navigate to frontend and install dependencies
cd hostel-management-mysql/frontend
npm install

# Start the Vite development server
npm run dev
```

---

### 2. Running Project 2 (`hostel-management-neo4j`)

```bash
# Navigate to backend and install dependencies
cd hostel-management-neo4j/backend
npm install

# Configure environment variables
cp ../.env.example .env
# Edit .env with your Neo4j AuraDB credentials:
# NEO4J_URI=neo4j+s://<your-instance-id>.databases.neo4j.io
# NEO4J_USERNAME=neo4j
# NEO4J_PASSWORD=your_neo4j_password_here

# Verify connection and start server
npm run test-connection
npm start
```

In a separate terminal:
```bash
# Navigate to frontend and install dependencies
cd hostel-management-neo4j/frontend
npm install

# Start the Vite development server
npm run dev
```

---

## 🌐 Deployment Architecture (Render & Vercel)

Both projects are designed to deploy independently to cloud infrastructure while residing within this monorepo:

### Project 1 — Aiven / Cloud MySQL
- **Render Backend Service**: Set **Root Directory** to `hostel-management-mysql/backend`
  - Build Command: `npm install`
  - Start Command: `npm start`
- **Vercel Frontend Project**: Set **Root Directory** to `hostel-management-mysql/frontend`
  - Framework Preset: `Vite`
  - Build Command: `npm run build`
  - Output Directory: `dist`
- **Database**: Aiven Cloud MySQL

### Project 2 — Neo4j AuraDB
- **Render Backend Service**: Set **Root Directory** to `hostel-management-neo4j/backend`
  - Build Command: `npm install`
  - Start Command: `npm start`
- **Vercel Frontend Project**: Set **Root Directory** to `hostel-management-neo4j/frontend`
  - Framework Preset: `Vite`
  - Build Command: `npm run build`
  - Output Directory: `dist`
- **Database**: Neo4j AuraDB

> **Important**: Existing deployment configurations remain completely separate and should NOT be modified until Root Directory adjustments are coordinated.

---

## 🔐 Security & Secrets Policy

- Real secrets (`.env`, `.env.local`, passwords, API tokens, Neo4j credentials, Aiven credentials) are strictly ignored by `.gitignore` and **must never be committed**.
- Use the `.env.example` template provided in each project directory as a reference for required environment variable keys.
