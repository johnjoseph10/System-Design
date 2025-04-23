# HA in Redis


## Redis Sentinel vs Redis Cluster

| Criteria                         | Redis Sentinel                  | Redis Cluster                          |
|----------------------------------|----------------------------------|----------------------------------------|
| Data fits on one node            | ✅ Yes                           | ❌ Not ideal                            |
| Need horizontal scalability      | ❌ No                            | ✅ Yes                                  |
| Simple architecture              | ✅ Yes                           | ❌ More complex                         |
| Multi-key operations (MGET, etc) | ✅ Easy                          | ⚠️ Limited across slots                |
| Requires custom client support   | ❌ No                            | ✅ Yes (cluster-aware)                  |
| Failover mechanism               | Sentinel + quorum               | Cluster + gossip + majority vote       |

---

## Usecases

   - Redis Sentinel :  For a system like a session store or config cache where data is small and fits on one node, Redis Sentinel is perfect. It provides automatic failover through a **quorum protocol** and is easy to integrate with standard Redis clients.

   - Redis Cluster :  Best for something like a real-time leaderboard or large-scale caching system. It uses a **gossip protocol** for node communication and automatically shards data across nodes. It enables horizontal scaling and high throughput.
