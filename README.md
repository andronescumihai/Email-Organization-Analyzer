# 📧 Email Organization Activity Analyzer

### 📊 Data Parsing & Statistical Aggregation
**Developed by Mihai-Alexandru Andronescu**

---

## 🚀 Overview
This project is designed to process large-scale email headers (`mbox` format) to identify and count the volume of communication originating from different organizations. It automates the extraction of domain information and provides a structured statistical breakdown of email activity.

## ✨ Key Features
* **Massive Text Parsing:** Efficiently reads and processes large `.txt` files containing thousands of email headers.
* **Domain Extraction Logic:** Uses Python's string manipulation and logic to isolate organizational domains from email addresses.
* **Relational Counting:** Implements an SQLite backend to perform "upsert" operations (Update or Insert) for real-time frequency tracking.
* **Data Persistence:** Stores results in a structured table (`Counts`), allowing for quick retrieval and sorting of the most active organizations.

## 🛠 Tech Stack
* **Language:** Python 3.x
* **Database:** SQLite (SQL-based aggregation)
* **Data Source:** Mbox (Standard Email Archive Format)

## 📂 Project Structure
* `orgcount.py`: The main script that performs parsing and database management.
* `mbox.txt`: The source dataset containing raw email header information.
* `orgdb.sqlite`: The generated database storing the organizational counts.

---
*Building efficient pipelines for data extraction and organizational intelligence.*
