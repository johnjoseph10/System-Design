
# 📖 What is Citus?

- Citus is an **open-source extension that turns PostgreSQL into a distributed, horizontally scalable database by sharding tables across multiple PostgreSQL instances.** It uses a coordinator-worker architecture to parallelize queries and scale both reads and writes.

- PostgreSQL is traditionally a single-node database. If the dataset grows beyond what one machine can handle (in terms of disk, memory, or CPU), vertical scaling becomes expensive and limited. To handle growing workloads or multi-tenant systems, we need horizontal scaling — and that's where Citus comes in."

- Citus distributes PostgreSQL tables across multiple nodes by sharding data based on a distribution key — like `customer_id` in a SaaS system. It converts Postgres into a distributed system while preserving the Postgres ecosystem, tooling, and SQL compatibility."

- **Coordinator node** handles query routing.
- **Worker nodes** each store a portion of the data.
- Queries like `SELECT * FROM contacts WHERE customer_id = 42` are routed directly to the worker containing that shard.
- Cross-customer queries run in parallel.

- The beauty of Citus is that you can add new worker nodes as your data grows and rebalance shards dynamically. It’s a practical way to scale Postgres horizontally without giving up its rich feature set.

- Citus essentially turns Postgres into a distributed, horizontally scalable database — ideal for multi-tenant SaaS, time-series, or real-time analytics workloads where scaling reads and writes across nodes is critical."
