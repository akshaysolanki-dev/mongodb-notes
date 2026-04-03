# 09-nodejs-integration/03-best-practices.md

# MongoDB + Node.js Best Practices (Deep)

## Introduction

Following best practices ensures:
- Better performance
- Cleaner code
- Scalability
- Security

---

## 1. Use Environment Variables

Never hardcode database URI.

---

### .env

```env
MONGO_URI=mongodb://127.0.0.1:27017
```

---

### Usage

```js
require("dotenv").config();

const client = new MongoClient(process.env.MONGO_URI);
```

---

## 2. Reuse Database Connection

### Bad Practice

```js
app.get("/", async () => {
  await client.connect();
});
```

---

### Good Practice

```js
await client.connect();

app.get("/", async () => {
  // reuse connection
});
```

---

## 3. Use Async/Await

Avoid callbacks.

---

### Good

```js
const data = await users.find().toArray();
```

---

## 4. Proper Error Handling

```js
try {
  await users.insertOne({ name: "Akshay" });
} catch (err) {
  console.error(err);
}
```

---

## 5. Use Indexes

- Improve query performance
- Use on frequently queried fields

---

## 6. Limit Data

Avoid fetching unnecessary data.

---

### Example

```js
await users.find({}, { name: 1 }).limit(10).toArray();
```

---

## 7. Validate Data

Use validation before inserting.

---

### Example

```js
if (!name) {
  throw new Error("Name is required");
}
```

---

## 8. Use Schema Validation (MongoDB)

```js
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name"]
    }
  }
});
```

---

## 9. Use Pagination

Avoid large queries.

---

```js
await users.find().skip(0).limit(10).toArray();
```

---

## 10. Avoid Large Documents

- Max size: 16MB
- Split large data

---

## 11. Use Aggregation Wisely

- Avoid unnecessary stages
- Use $match early

---

## 12. Secure Your Database

- Use authentication
- Restrict access
- Avoid public exposure

---

## 13. Logging

Log important operations.

```js
console.log("User created");
```

---

## 14. Use Connection Pooling

MongoDB driver handles pooling automatically.

---

## 15. Close Connection Properly

```js
await client.close();
```

---

## 16. Avoid Blocking Operations

- Keep queries efficient
- Avoid heavy computations in DB

---

## 17. Use Transactions (When Needed)

```js
const session = client.startSession();
```

---

## 18. Use Consistent Naming

- collection names → plural
- fields → camelCase

---

## 19. Separate Logic

- DB logic separate from routes
- Use services or controllers

---

## 20. Monitor Performance

- Use explain()
- Track slow queries

---

## Real World Structure

```bash
project/
├── db/
│   └── connection.js
├── models/
├── controllers/
├── routes/
```

---

## Summary

- Use env variables
- Reuse connections
- Use async/await
- Validate and secure data
- Optimize queries
- Follow clean architecture