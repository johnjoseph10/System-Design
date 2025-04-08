# Web Crawler

## Clarifying Questions to Ask

1. Are we crawling the entire web or specific domains, and are we dealing with potentially billions of pages ( entire web)?  
2. Are we building a search index, extracting data for analytics, training LLMs, or another purpose?  
3. Which page elements need to be collected (URLs, titles, meta tags, full text), and do we need OCR for images? or how to extract javascript loaded pages?
4. Must we respect robots.txt and other politeness constraints?  
5. How should we store or process data (raw HTML vs. parsed content), and do we need to resume from checkpoints?  
6. Is this a one-time crawl or a continuous process for updates?  

## Functional Requirements

1. Crawl URLs from an initial list of seed URLs
2. Store the webpage data
3. Extract additional URLs from the webpages and add them to the seed list

## Non functional Requirements

1. Must scale to handle the entire World Wide Web
2. Built-in fault tolerance
3. Schedule periodic updates to keep retrieved data current
4. Respect robots.txt for politeness
5. Observability/Logs/Metrics

## Design Diagram

[![Web Crawler Diagram](./wc.jpg)](https://lucid.app/documents/embedded/bf389c44-10bc-45b4-a083-8c131a29b1d4)





## Crawler and HTML Parser: Separation of Duties

While the crawler **can** perform HTML parsing, separating the crawler and the HTML parser has several advantages:

1. **Improved system design** – it allows each component to scale independently.  
2. **Fault isolation** – a failure in one stage does not disrupt the entire system.  
3. **Independent optimization** – each stage can be scaled or optimized on its own.  
4. **Checkpointing** – data from successful stages is already stored, allowing you to resume from where you left off.



### 🛡️ Fault Tolerance

#### 1. URL Not Reachable

Implement a **retry mechanism** for failed URL fetch attempts.

**Retry Options (with trade-offs):**

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **Memory Timer** | Retry in-memory with a timer | - Simple to implement<br>- No extra infrastructure | - Lost on process crash<br>- Doesn't persist across restarts |
| **Kafka with Custom Exponential Backoff** | Implement backoff logic in consumer code | - Full control over retry logic<br>- Durable messaging | - Requires custom implementation<br>- More operational complexity |
| **SQS with Built-in Exponential Backoff** | Leverage AWS SQS delay queues and retries | - Built-in support<br>- Easy to configure<br>- Durable | - Less control over retry behavior<br>- AWS-dependent |

---

#### 2. Crawler Is Down

- A new crawler instance will automatically spin up based on the **Auto Scaling Group (ASG)** configuration.
- **What happens to in-flight messages?**  
  Messages will remain in the queue (Kafka/SQS) based on the action defined (e.g., visibility timeout, redelivery policy), ensuring no data loss.

#### 3. DNS Is Not Available

- A backup DNS will serve the purpose

#### 4. Message Retention When the Crawler Is Down

- **Kafka**:
  - Messages are retained based on the configured **retention period** (e.g., 7 days by default).
  - As long as the retention window is not exceeded, the new crawler instance can pick up where the previous  committed offset 

- **SQS**:
  - Messages stay in the queue for up to **14 days** (maximum retention).
  - Messages not acknowledged (visibility timeout) will be retried.


## 🧠 Duplicate Detection (Trade-offs)

| **Category**         | **Method**                     | **Pros**                                                                 | **Cons**                                                                 |
|----------------------|--------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Duplicate URLs**   | **DB Primary Key (URL Table)** | - Simple to implement<br>- Persistence guaranteed                        | - Slow at scale<br>- DB bottleneck risk                                  |
|                      | **Bloom Filter**               | - Fast, in-memory<br>- Very low memory usage                             | - False positives<br>- No deletions supported                            |
|                      | **Redis Set**                  | - Fast lookups<br>- Persistent (if needed)<br>- Easy to scale            | - Memory usage grows with data<br>- Requires Redis setup and maintenance |
| **Duplicate Content**| **Hash Column in Domain Table**| - Reliable hash-based comparison<br>- Leverages existing DB structure     | - Slower at scale<br>- Increases DB load                                 |
|                      | **Redis Set (Content Hashes)** | - Very fast lookups<br>- Scales well<br>- Good for high-volume systems   | - High memory usage<br>- Requires Redis infrastructure                   |
|                      | **Bloom Filter (Content Hashes)**| - Extremely memory-efficient<br>- Very fast checks                      | - False positives<br>- No actual data retrievable<br>- No deletions      |



## Scalability

