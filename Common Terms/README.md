# Common Terms 

## Fan-out on Read / Fan-out on Write

### 📱 Facebook News Feed – Fan-out on Write (with Exception)

Facebook mostly uses **fan-out on write** for the News Feed. When a user posts something, the system **immediately pushes it to the feeds of their friends**, so the post is ready to read without delay.

This works well for regular users because:

- ✅ Feeds load quickly  
- ✅ Efficient for read-heavy traffic  
- ✅ Allows per-user personalization at write time  

### ❗ Exception: High-Follower Users

For celebrities or influencers with **millions of followers**, Facebook **does not use fan-out on write**. Instead, it switches to **fan-out on read** — meaning the post is fetched and shown dynamically when followers check their feeds. This avoids overwhelming the system with millions of write operations for one post.

### ⚖️ Hybrid Model Summary

- **Regular users** → *Fan-out on write*  
- **High-follower users** → *Fan-out on read*




## Sharding in Databases

### What is Sharding?

**Sharding** is a database partitioning technique that distributes data across multiple servers. It helps manage large datasets and improves performance by reducing the load on a single server.

---

### Sharding a Table by `userId`

Sharding a table by `userId` splits data into different partitions based on the `userId` field, improving scalability and performance.

#### Steps to Shard by `userId`:

1. **Choose a Sharding Strategy**  
   - **Hash-based**: Use a hash function on `userId` to determine the shard.
   - **Range-based**: Divide `userId` into ranges and assign them to different shards.

2. **Create Shard Key**  
   The `userId` becomes the shard key, which will determine where each record is stored.

3. **Shard Mapping Logic**
   - **Hash-based**: `SELECT MOD(userId, num_shards)`
   - **Range-based**: Define ranges like `WHERE userId BETWEEN 1 AND 1000`.

4. **Insert Data**
   Direct data to the correct shard based on `userId`.

5. **Query Management**
   Use routing logic to direct queries to the correct shard. Cross-shard queries may require aggregation.

6. **Shard Rebalancing**
   As data grows, you might need to add more shards or redistribute data.

---

### Benefits of Sharding

- **Improved Performance**: Faster reads and writes by distributing data.
- **Scalability**: Easier to scale horizontally as data grows.
- **Fault Isolation**: Shard failures affect only a portion of data.

---

### Considerations

- **Complexity**: Managing multiple shards can be challenging, especially for cross-shard queries.
- **Consistency**: Maintaining consistency across shards requires careful transaction management.

