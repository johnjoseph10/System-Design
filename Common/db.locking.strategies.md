# Optimistic Concurrency Control (OCC)

## 🔍 What is OCC?

**Optimistic Concurrency Control** is a way to **manage simultaneous transactions** in a system **without using locks**. It assumes that **most of the time, conflicts between users or transactions won’t happen**, so instead of blocking others, it lets everyone proceed and **only checks for conflicts at the end**—when the transaction is ready to commit.

---

## ✅ How OCC Works (3 Phases)

1. **Read Phase**  
   - A transaction reads the data and does its processing.  
   - No locks are placed.  
   - A copy of the data (often with a version number or timestamp) is stored.

2. **Validation Phase**  
   - Before committing, the system checks whether the data **was changed** by another transaction since it was read.  
   - If no one else touched the data → ✅ safe to commit.  
   - If someone **did** change the data → ❌ conflict → the transaction is rolled back and retried.

3. **Write Phase**  
   - If validation passes, the transaction writes its changes to the database.

---

## 🔧 What Makes OCC “Optimistic”?

Because it **optimistically assumes** that data conflicts are **rare**, it avoids the overhead of locking data upfront. This improves performance and allows for greater concurrency in **read-heavy or low-contention systems**.

---

## 🛒 Real-World Analogy

Imagine you're filling out a form at the DMV:

- You grab a blank form and fill it out (**read phase**).
- Just before submitting it, you check whether the form version has changed (**validation**).
- If everything's still valid, you submit it (**write phase**).
- But if the DMV updated the form while you were filling it out, you have to start over (**rollback**).

---

## 🏁 When to Use OCC

- Systems with **many reads** and **fewer writes**
- Applications where **conflicts are rare**

**Examples**:
- Shopping carts
- Reservation systems
- Reporting dashboards
- Mobile apps syncing data

---

## ⚠️ Trade-offs

| Pros                               | Cons                                           |
|------------------------------------|------------------------------------------------|
| No locking → better performance    | Higher chance of rollbacks if conflicts happen |
| Scales well with read-heavy loads  | Not ideal for high-contention systems          |
