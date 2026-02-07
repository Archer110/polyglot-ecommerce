
# NEXUS - Polyglot E-Commerce Platform

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Flask](https://img.shields.io/badge/Flask-3.0-green)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue)
![MongoDB](https://img.shields.io/badge/MongoDB-6.0-green)
![HTMX](https://img.shields.io/badge/HTMX-1.9-orange)

**NEXUS** is a modern, high-performance e-commerce platform built to demonstrate **Polyglot Persistence** architecture. It leverages the strengths of both SQL and NoSQL databases to handle different types of data optimally, bridged by a robust Python Service Layer.

## 🚀 Key Features

### 1. Polyglot Persistence Architecture

- **MongoDB (Catalog):** Stores flexible, document-based product data. Allows for dynamic specifications (e.g., Laptops have "RAM", T-Shirts have "Size") without complex join tables.
- **PostgreSQL (Commerce):** Stores structured, transactional order data. Ensures ACID compliance for financial integrity and relational mapping for customers.

### 2. The "Modern Monolith" Frontend

- **HTMX:** Delivers SPA-like interactivity (instant search, dynamic cart drawer) without the complexity of a separate frontend framework (React/Vue).
- **Alpine.js:** Manages client-side state for UI components like modals and transitions.
- **Tailwind CSS:** Utilizes a custom "Neo-Brutalism" design system.

### 3. Service Layer Design Pattern

- **Decoupled Logic:** Business logic is strictly separated from HTTP routes, making the codebase testable and agnostic to the frontend interface.
- **Unified Data Model:** The application layer performs "logical joins" to merge data from SQL and NoSQL sources seamlessly.

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Backend** | Python 3.12, Flask |
| **Database (SQL)** | PostgreSQL (via SQLAlchemy) |
| **Database (NoSQL)** | MongoDB (via PyMongo) |
| **Frontend** | Jinja2, HTMX, Alpine.js, TailwindCSS |
| **Tooling** | UV (Package Manager), Ruff (Linter), Makefile |

---

## ⚡ Setup & Installation

### Prerequisites

- Python 3.10+
- PostgreSQL (Running locally on port 5432)
- MongoDB (Running locally on port 27017)

### 1. Clone & Install

```bash
git clone [https://github.com/Archer110/nexus.git](https://github.com/Archer110/nexus.git)
cd nexus

# Install dependencies (Using UV is recommended for speed)
pip install uv
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
uv pip install -r requirements.txt

```

### 2. Environment Configuration

Create a `.env` file in the root directory:

```bash
cp .env.example .env

```

*Edit `.env` to match your local database credentials if they differ from the defaults.*

### 3. Database Initialization

Use the provided `Makefile` shortcuts to set up the databases:

```bash
# Initialize and Upgrade SQL Migrations
make db-init
make db-migrate
make db-upgrade

# Seed the Database (Populates Products first, then Orders)
make seed

```

### 4. Run the Application

```bash
make run

```

The application will start at `http://localhost:5000`.

---

## 📂 Project Structure

```text
nexus/
├── app/
│   ├── models/         # Data Access Layer (SQL & Mongo Definitions)
│   ├── routes/         # Presentation Layer (Traffic Control)
│   ├── services/       # Business Logic Layer (The "Brain")
│   └── templates/      # Jinja2 HTML Templates
├── migrations/         # Alembic SQL Migrations
├── static/             # CSS, JS, Images
├── .env.example        # Environment Variable Template
├── Makefile            # Command Shortcuts
├── README.md           # Documentation
├── requirements.txt    # Python Dependencies
└── run.py              # Application Entry Point

```

## 🧪 Key Query Patterns (For Developers)

**1. The Hybrid Merge (Service Layer)**
*Fetching an order involves querying Postgres for the transaction ID, then querying Mongo for the product details using the stored reference IDs.*

**2. Faceted Search (MongoDB)**
*Filtering products by dynamic attributes (e.g., `specs.RAM=16GB`) uses MongoDB's flexible schema capabilities.*

**3. Atomic Transactions (PostgreSQL)**
*Checkout operations are wrapped in a SQLAlchemy transaction block to ensure that Order and OrderItem records are created simultaneously or not at all.*

---

## 📜 License

MIT License.
