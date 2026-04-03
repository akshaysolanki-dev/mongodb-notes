# 09-nodejs-integration/01-connection.md

# MongoDB Connection with Node.js (Deep)

## Introduction

To use MongoDB in a backend application, we connect it with Node.js.

Official driver:
- mongodb (Node.js driver)

---

## Installation

```bash
npm install mongodb
```

---

## Import MongoClient

```js
const { MongoClient } = require("mongodb");
```

---

## Connection URL

Default local connection:

```js
mongodb://127.0.0.1:27017
```

---

## Basic Connection

```js
const client = new MongoClient("mongodb://127.0.0.1:27017");

async function connectDB() {
  await client.connect();
  console.log("Connected to MongoDB");
}

connectDB();
```

---

## Access Database

```js
const db = client.db("myDatabase");
```

---

## Access Collection

```js
const users = db.collection("users");
```

---

## Full Example

```js
const { MongoClient } = require("mongodb");

const client = new MongoClient("mongodb://127.0.0.1:27017");

async function run() {
  try {
    await client.connect();

    const db = client.db("testDB");
    const users = db.collection("users");

    const result = await users.find().toArray();
    console.log(result);

  } catch (err) {
    console.error(err);
  } finally {
    await client.close();
  }
}

run();
```

---

## Async/Await Importance

MongoDB operations are asynchronous.

Always use:
- async/await
- or promises

---

## Error Handling

```js
try {
  await client.connect();
} catch (error) {
  console.error("Connection failed:", error);
}
```

---

## Environment Variables (Best Practice)

Install dotenv:

```bash
npm install dotenv
```

---

### .env file

```env
MONGO_URI=mongodb://127.0.0.1:27017
```

---

### Use in Code

```js
require("dotenv").config();

const client = new MongoClient(process.env.MONGO_URI);
```

---

## Connection Options

```js
const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

---

## Reusing Connection (Important)

Do NOT create connection repeatedly.

---

### Bad Practice

```js
app.get("/", async () => {
  await client.connect();
});
```

---

### Good Practice

- Connect once
- Reuse client

---

## Connection Pooling

MongoDB automatically manages connection pool.

Benefits:
- Efficient resource usage
- Faster queries

---

## Close Connection

```js
await client.close();
```

---

## Important Notes

- Always handle errors
- Do not expose connection string
- Use environment variables

---

## Real World Example

```js
const db = client.db("ecommerce");
const products = db.collection("products");

const data = await products.find().toArray();
```

---

## Summary

- Use MongoClient to connect
- Use async/await
- Store URI in .env
- Reuse connection
- Handle errors properly