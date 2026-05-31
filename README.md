# 📧 Email Organization Activity Analyzer

> **Python for Everybody — University of Michigan** | SQLite + mbox Data Processing

---

## 📌 Project Overview

A Python script that parses large-scale **mbox email archives**, extracts organizational domains from sender addresses, and persists frequency counts in a **SQLite database** using an upsert pattern (INSERT or UPDATE). The result is a ranked leaderboard of the most active organizations in the dataset.

Built as part of the *Python for Everybody* specialization (University of Michigan / Coursera), simulating a real data engineering task: ingesting unstructured text, normalizing it, and surfacing actionable insights through structured storage and SQL queries.

---

## ✨ Key Features

| Feature | Implementation |
|---|---|
| 📂 **mbox Parsing** | Line-by-line file iteration, filtering only `From:` header lines |
| 🔍 **Domain Extraction** | `split('@')[1]` — isolates organizational domain from full email address |
| 🗄️ **SQLite Upsert Logic** | `SELECT` → `INSERT` if not found, `UPDATE count + 1` if exists — manual upsert without ORM |
| 📊 **Ranked Output** | `ORDER BY count DESC LIMIT 10` — top 10 most active organizations |
| 💾 **Data Persistence** | Results stored in `orgdb.sqlite` — queryable after script completion |
| 🔄 **Idempotent Execution** | `DROP TABLE IF EXISTS` + `CREATE TABLE` on every run — clean slate guaranteed |

---

## 🛠️ Tech Stack

- **Language:** Python 3.x
- **Database:** SQLite3 (standard library — no external dependencies)
- **Data Source:** mbox format (standard email archive)
- **Course:** Python for Everybody — University of Michigan (Coursera)

---

## 📁 Repository Structure

```
├── orgcount.py      # Main script: parse → extract → upsert → query
├── mbox.txt         # Source dataset: raw email headers in mbox format
└── orgdb.sqlite     # Generated database: Counts table (org TEXT, count INTEGER)
```

---

## ⚙️ How It Works

```python
# Core logic — for each "From:" line:
email = line.split()[1]          # Extract email address
domain = email.split('@')[1]     # Extract domain (e.g. "umich.edu")

# Upsert pattern:
cur.execute('SELECT count FROM Counts WHERE org = ?', (domain,))
row = cur.fetchone()
if row is None:
    cur.execute('INSERT INTO Counts (org, count) VALUES (?, 1)', (domain,))
else:
    cur.execute('UPDATE Counts SET count = count + 1 WHERE org = ?', (domain,))

# Final query — top 10 orgs:
SELECT org, count FROM Counts ORDER BY count DESC LIMIT 10
```

---

## ▶️ How to Run

```bash
# Requirements: Python 3.x only (no pip installs needed)
python3 orgcount.py
```

Outputs top 10 organizations by email volume directly to console. Database saved to `orgdb.sqlite`.

---

## 🧠 What I Learned

- Parsing **real-world unstructured text formats** (mbox) with efficient line-by-line iteration
- Implementing **manual upsert logic** in SQLite without ORMs — understanding the SELECT → INSERT/UPDATE pattern
- Using **parameterized SQL queries** (`?` placeholders) to prevent SQL injection
- Designing **idempotent scripts** that produce consistent results on repeated execution
- Connecting Python data processing to **persistent relational storage** via `sqlite3`

---

## 📜 Context

Part of the **Python for Everybody** specialization by Dr. Charles Severance (University of Michigan), specifically the *Using Databases with Python* course. The exercise simulates real data pipeline work: ingesting raw logs, normalizing entities, and producing ranked analytics — a pattern used in production data engineering.

---

## 👤 Author

**Mihai-Alexandru Andronescu**
Student — Computer Science & Economics, ASE Bucharest

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/mihai-alexandru-andronescu-58792b33b/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-black?logo=github)](https://github.com/andronescumihai)
