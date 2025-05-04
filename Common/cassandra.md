
# Cassandra for Event Storage – Simple Guide

---

## ✅ What We're Doing

- Storing lots of fast-moving data (like user clicks or actions).
- This is called an **event stream**.
- We need a database that can **handle high write speeds**.

---

## 🔧 Why Use Cassandra?

- **Optimized for writing** large amounts of data.
- **Highly scalable** and reliable.
- Built for **speed and volume**, not complex queries.

---

## 🧪 How Cassandra Stores Data

- **Memtable**: Fast in-memory storage for new data.
- **Commit Log**: Backup in case of crashes.
- **SSTable**: Periodically saved files on disk.

🔁 It works like a **logbook** — always writing new entries, not editing old ones.

---

## ⚠️ What Cassandra Isn’t Great At

**Good for:**
- Getting one specific row (e.g., “What did user123 do?”)

**Not good for:**
- Range queries or summaries like:
  - “How many clicks last hour?”
  - “Most popular action today?”

📌 Reason: Data is **spread across many files**, not easy to scan or count.
