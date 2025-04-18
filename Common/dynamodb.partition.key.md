*Partition Key in DynamoDB**

- A **partition key** determines **where** data is stored in DynamoDB.
- It uniquely identifies each item (or group of items).
- DynamoDB uses it to **distribute data** across storage nodes.

### 🔹 Key Types:

1. **Partition Key (Simple Primary Key)**
   - Uniquely identifies each item.
   - Example:
     ```json
     {
       "UserID": "user123"
     }
     ```

2. **Composite Key (Partition Key + Sort Key)**
   - Groups related items by partition key.
   - Sort key makes each item within the group unique.
   - Example:
     ```json
     {
       "UserID": "user123",
       "OrderID": "order456"
     }
     ```

### ✅ Best Practices:
- Use a partition key with **high cardinality**.
- Avoid "hot keys" to maintain even data distribution.


### 🧩 When to Use a Composite Key in DynamoDB

- You want to **store multiple related items** under the same partition.
- You need to **query efficiently within a group** of related items.

### ✅ Common Use Cases:

1. **User and Orders**
   - Partition Key: `UserID`
   - Sort Key: `OrderID`
   - Query all orders for a specific user.

2. **Device and Timestamps**
   - Partition Key: `DeviceID`
   - Sort Key: `Timestamp`
   - Query sensor readings in a time range for one device.

3. **Project and Tasks**
   - Partition Key: `ProjectID`
   - Sort Key: `TaskID` or `DueDate`
   - Fetch all tasks for a project, sorted by due date.

### 🧠 Why It's Useful:
- Enables **range queries** on the sort key.
- Keeps related data **grouped and ordered**.
- Reduces need for secondary indexes.
