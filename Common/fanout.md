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