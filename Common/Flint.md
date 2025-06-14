# Zookeeper Overview

## 1. zNodes

Zookeeper stores data in a tree-like structure, where each node is called a **zNode**. There are three main types:

- **Persistent zNodes**  
  These stay in Zookeeper until explicitly deleted, even if the client disconnects.

- **Ephemeral zNodes**  
  These are tied to the client's session and are automatically removed when the session ends.

- **Sequential zNodes**  
  These get a unique, incrementing number added to their name. Useful for things like queues or locks.

---

## 2. Ensemble – Avoiding SPOF

A **Zookeeper Ensemble** is a group of Zookeeper servers that work together to ensure availability and reliability.

- Helps avoid a **single point of failure (SPOF)**
- Requires a **majority (quorum)** of nodes to agree on changes
- Typically uses an **odd number** of nodes (e.g., 3, 5) to handle failures cleanly

---

## 3. Watch Mechanism

Zookeeper supports a **watch** mechanism that simplifies communication:

- Servers register interest (watches) in certain zNodes.
- When data changes, only the **interested servers** are notified.
- This eliminates the need for every server to connect to every other server (avoiding **n²** complexity).

This setup is lightweight and scalable.

---

## 4. Real-World Example: Chat Application

In a distributed chat system:

- **Servers** register themselves with Zookeeper.
- **Users** are assigned to servers using a **hash function** based on user ID.
- Zookeeper only tracks **server state**, not individual users.

This makes Zookeeper a lightweight metadata service that keeps the system dynamic and scalable.
