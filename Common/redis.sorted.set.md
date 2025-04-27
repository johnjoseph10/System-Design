
# Redis Sorted Set

A **Sorted Set** in Redis is like a regular set, but every member has a **numeric score**.  
Redis keeps members **sorted by their score** — which makes it great for **ranking, prioritizing, and ordering**.

**Key Properties:**
- Each value is unique.
- Each value has a score (floating-point).
- Sorted by score, either ascending or descending.
- A ZSET is Redis’s name for a Sorted Set data structure.

---

## 🔧 Quick Commands

| Operation             | Command Example                                      |
|:---------------------|:-----------------------------------------------------|
| Add member with score | `ZADD leaderboard 200 "Alice"`                       |
| Get top N members     | `ZREVRANGE leaderboard 0 2 WITHSCORES`               |
| Get member's rank     | `ZREVRANK leaderboard "Alice"`                       |
| Increment score       | `ZINCRBY leaderboard 50 "Alice"`                     |
| Remove member         | `ZREM leaderboard "Alice"`                           |

---

## 📌 Where It’s Used in System Design

Sorted Sets shine when you need **fast, ranked, or time-ordered data retrieval**. Here’s where it shows up:

### 🎮 1️⃣ Leaderboards
Keep a **real-time ranking of players** based on their scores. Your application defines and computes the value/score, then stores it in Redis. Redis handles sorting and ranking, not scoring logic.
- `ZADD` when a player finishes a game.
- `ZREVRANGE` to get top 10 players.

---

### 📅 2️⃣ Time-Based Queues / Scheduling
Use timestamps as scores for **delayed jobs, scheduled tasks**.
- `ZADD` job with a future timestamp.
- `ZRANGEBYSCORE` to fetch due jobs.

---

### 📊 3️⃣ Rate Limiting
Track **actions per user per time window**.
- `ZADD` with current timestamp.
- `ZREMRANGEBYSCORE` to remove old actions.
- `ZCARD` to count how many actions left.

---

### 🎵 4️⃣ Real-Time Trending / Popularity Feeds  
Track which posts, songs, or articles are getting the most interactions **right now**.
- `ZINCRBY` when someone likes/views a post.
- `ZREVRANGE` to fetch trending content.

---

## ⚡ Why Use It?
- **O(log N)** insertion and removal.
- Ordered retrieval without extra sorting.
- Clean API for rankings, limits, scheduling.

---

## 📌 Final Thought
Redis Sorted Sets are **crazy efficient for ranked or ordered lists** where you also need to query by rank or score range — making them a favorite in system designs for **leaderboards, rate limiting, scheduling, and trending feeds**.
