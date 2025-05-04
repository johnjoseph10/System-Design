
#  What Is Apache Spark?

Apache Spark is a powerful engine for big data processing. It helps you:

- Read massive amounts of data (from Cassandra, HDFS, S3, etc.)
- Clean, transform, and analyze it in memory (super fast)
- Run tasks in parallel across a cluster of machines
- Build real-time or batch data pipelines

---

## ⚙️ What Apache Spark Does (Simple Summary)

| Task                      | What Spark Does                                     |
|---------------------------|------------------------------------------------------|
| ETL (Extract, Transform, Load) | Cleans and transforms huge datasets             |
| Aggregation               | Groups and summarizes large-scale data              |
| Machine Learning          | Runs algorithms on big data (clustering, models)    |
| Streaming                 | Processes live data (e.g., clickstream)             |
| SQL Queries               | Lets you run SQL over giant datasets                |

---

## 📦 Real-World Example: Page Click Aggregation

### Problem:
You have millions of click events in Cassandra and want to know:

> “How many clicks did each page get in the last hour?”

### Spark’s Role:
- Reads click events from Cassandra.
- Filters to the last hour.
- Groups by page.
- Counts clicks per page.
- Writes the result back to Cassandra.
