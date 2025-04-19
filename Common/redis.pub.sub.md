## Redis Pub/Sub

Redis Pub/Sub (short for **Publish/Subscribe**) is a messaging pattern built into Redis that allows real-time communication between services, apps, or components.

---

## 🔁 How It Works

- A **Publisher** sends a message to a **channel**.  
- **Subscribers** listen to that channel and receive any messages published to it instantly.

It’s like a radio:

- One station broadcasts (publishes),  
- Anyone tuned in (subscribed) hears the message.

---

## 💡 Use Cases

- Real-time notifications (chat apps, dashboards)  
- Event broadcasting (e.g., new auction bids, status updates)  
- Decoupling microservices  
- Triggering background jobs
