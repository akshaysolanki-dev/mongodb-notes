# 09-nodejs-integration/02-crud-with-node.md

# CRUD Operations with Node.js (Deep)

## Introduction

Using MongoDB with Node.js allows performing CRUD operations programmatically.

We use:
- MongoClient
- async/await

---

## Setup

```js
const { MongoClient } = require("mongodb");

const client = new MongoClient("mongodb://127.0.0.1:27017");
```

---

## Connect to Database

```js
await client.connect();

const db = client.db("testDB");
const users = db.collection("users");
```

---

## CREATE (Insert)

### insertOne()

```js
await users.insertOne({
  name: "Akshay",
  age: 25
});
```

---

### insertMany()

```js
await users.insertMany([
  { name: "A", age: 20 },
  { name: "B", age: 30 }
]);
```

---

## READ (Find)

### find()

```js
const data = await users.find().toArray();
console.log(data);
```

---

### findOne()

```js
const user = await users.findOne({ name: "Akshay" });
console.log(user);
```

---

## READ with Filter

```js
const data = await users
  .find({ age: { $gt: 20 } })
  .toArray();
```

---

## UPDATE

### updateOne()

```js
await users.updateOne(
  { name: "Akshay" },
  { $set: { age: 26 } }
);
```

---

### updateMany()

```js
await users.updateMany(
  { age: { $gt: 20 } },
  { $set: { status: "active" } }
);
```

---

## DELETE

### deleteOne()

```js
await users.deleteOne({ name: "Akshay" });
```

---

### deleteMany()

```js
await users.deleteMany({ age: { $lt: 18 } });
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

    // CREATE
    await users.insertOne({ name: "Akshay", age: 25 });

    // READ
    const allUsers = await users.find().toArray();
    console.log(allUsers);

    // UPDATE
    await users.updateOne(
      { name: "Akshay" },
      { $set: { age: 26 } }
    );

    // DELETE
    await users.deleteOne({ name: "Akshay" });

  } catch (error) {
    console.error(error);
  } finally {
    await client.close();
  }
}

run();
```

---

## Important Notes

- Always use await with DB operations
- Convert cursor to array using toArray()
- Use proper filters

---

## Common Mistakes

### Forgetting await

```js
users.find(); // ❌
```

---

### Correct

```js
await users.find().toArray();
```

---

## Error Handling

```js
try {
  await users.insertOne({ name: "Akshay" });
} catch (err) {
  console.error(err);
}
```

---

## Performance Tips

- Use indexes for queries
- Avoid fetching unnecessary data
- Use limit() when needed

---

## Real World Example

```js
const products = db.collection("products");

const topProducts = await products
  .find({ category: "Electronics" })
  .sort({ price: -1 })
  .limit(5)
  .toArray();
```

---

## Summary

- Use MongoClient with async/await
- Perform CRUD using collection methods
- Handle errors properly
- Optimize queries for performance