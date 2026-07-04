# 🎓 University Database

A fully relational **university management database** built from the ground up using pure **SQL**. This project models the real-world complexity of a university — from classrooms and departments to students, instructors, courses, grades, and academic prerequisites — all wired together through a robust, normalized schema.

---

## ⚡ Tech Stack

| Technology | Purpose |
|---|---|
| **SQL** | Schema design, data definition, and data manipulation |
| **DDL (Data Definition Language)** | Table creation with constraints, primary keys, and foreign keys |
| **DML (Data Manipulation Language)** | Seeding and managing relational data |
| **Relational Database Model** | Normalized multi-table design with cascading rules |

Compatible with any standard SQL database engine — **PostgreSQL**, **MySQL**, **SQLite**, or **Oracle DB**.

---

## 🗄️ Schema Overview

The database is built on **11 interconnected tables** that mirror how a real university operates:

```
classroom ──────────────────────────────────────┐
department ──┬── course ──┬── section ──┬── teaches ── instructor
             │            │             └── takes ──── student ── advisor
             └── instructor            
                          └── prereq (self-referencing)
time_slot ──────────────────────────────────────┘
```

### Tables
- **`classroom`** — Buildings, room numbers, and seating capacities
- **`department`** — Academic departments with budget tracking
- **`course`** — Course catalogue with credit hours and department ownership
- **`instructor`** — Faculty records with salary and department assignment
- **`section`** — Scheduled course sections by semester and year
- **`teaches`** — Many-to-many mapping of instructors to sections
- **`student`** — Student records with cumulative credit tracking
- **`takes`** — Enrollment and grade records per student per section
- **`advisor`** — Student–instructor advisory relationships
- **`time_slot`** — Scheduled meeting times with day/hour/minute precision
- **`prereq`** — Course prerequisite chains (self-referencing foreign key)

---

## 🔒 Data Integrity Highlights

This schema is engineered for **rock-solid referential integrity**:

- ✅ **Primary keys** on every table — no ambiguous records
- 🔗 **Foreign keys with cascade rules** — `ON DELETE CASCADE` and `ON DELETE SET NULL` keep data consistent automatically
- 🛡️ **CHECK constraints** enforce business logic:
  - Instructor salaries must exceed `$29,000`
  - Department budgets must be positive
  - Semesters are restricted to `Fall`, `Winter`, `Spring`, or `Summer`
  - Academic years are bounded between `1701` and `2100`
  - Time slot hours and minutes are validated ranges

---

## 📦 Files

| File | Description |
|---|---|
| `DDL+drop.sql` | Drops existing tables and rebuilds the full schema from scratch |
| `smallRelationsInsertFile.sql` | Seeds the database with a realistic sample dataset |

---

## 🚀 Getting Started

1. **Clone the repo**
   ```bash
   git clone https://github.com/MaxKarltun/University-Database.git
   cd University-Database
   ```

2. **Run the schema setup** (creates all tables)
   ```bash
   psql -U youruser -d yourdb -f "DDL+drop.sql"
   ```

3. **Seed the database** (loads sample data)
   ```bash
   psql -U youruser -d yourdb -f smallRelationsInsertFile.sql
   ```

4. **Start querying!** Explore departments, enrolments, grades, prerequisites and more.

---

## 🧩 Sample Data Includes

- **7 departments** — Comp. Sci., Physics, Biology, Finance, History, Music, Elec. Eng.
- **13 courses** — from *Game Design* and *Robotics* to *Investment Banking* and *Genetics*
- **12 instructors** and **13 students** with real academic relationships
- **Full enrollment history** with letter grades across multiple semesters
- **Prerequisite chains** linking foundational courses to advanced ones

---

## 📚 Based On

Schema design inspired by the classic university database from **"Database System Concepts"** by Silberschatz, Korth & Sudarshan — the gold standard textbook for relational database theory.
