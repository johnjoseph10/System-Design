# Zookeeper Overview

## zNodes

Zookeeper stores all its data in a hierarchical namespace, similar to a file system. Each node in this tree is referred to as a **zNode**.

### Types of zNodes

- **Persistent zNodes**  
  These remain in Zookeeper until explicitly deleted, regardless of client session state.

- **Ephemeral zNodes**  
  These are tied to the lifecycle of a client session and are automatically removed when the session ends.

- **Sequential zNodes**  
  When a zNode is created with the sequential flag, Zookeeper appends a monotonically increasing counter to its name, useful for queues and locks.

---

## Real-World Use Case: Chat Application

In a scalable chat application:

- **Servers** register themselves in Zookeeper.
- **Users** are assigned to servers using a **hash function** based on their user ID.
- Zookeeper tracks **only the servers**, not each individual user.
- This approach minimizes overhead and keeps the metadata layer lightweight.

---

## Ensemble

A **Zookeeper Ensemble** is a group of Zookeeper servers working together.

- Ensures **high availability**
- Avoids a **single point of failure (SPOF)**
- Requires a **quorum** (majority) for writes

> Typically, an odd number of servers (e.g., 3, 5, 7) is used to ensure fault tolerance.

