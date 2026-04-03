# 10-real-world/01-user-system-design.md

# User System Design (MongoDB Real World)

## Introduction

This section explains how to design a real-world user system using MongoDB.

We will cover:
- User schema
- Relationships
- Best practices
- Scalability considerations

---

## Basic User Schema

```json
{
  "_id": ObjectId("..."),
  "name": "Akshay",
  "email": "akshay@email.com",
  "password": "hashed_password",
  "age": 25,
  "isActive": true,
  "createdAt": ISODate("2025-01-01T00:00:00Z")
}
```

---

## Important Fields

- name → user name
- email → unique identifier
- password → hashed (never store plain text)
- isActive → account status
- createdAt → timestamp

---

## Indexing (Very Important)

```js
db.users.createIndex({ email: 1 }, { unique: true })
```

---

## Authentication Flow (Concept)

1. User registers
2. Password is hashed
3. Data stored in MongoDB
4. User logs in
5. Password compared

---

## Password Storage (Important)

Never store plain passwords.

Use hashing:

```js
bcrypt.hash(password, 10)
```

---

## Login Query

```js
const user = await users.findOne({ email: email });
```

---

## User Profile Update

```js
await users.updateOne(
  { _id: userId },
  { $set: { name: "New Name" } }
);
```

---

## Soft Delete

Instead of deleting user:

```js
await users.updateOne(
  { _id: userId },
  { $set: { isActive: false } }
);
```

---

## Relationships

### User with Orders (Reference)

Users Collection:

```json
{
  "_id": 1,
  "name": "Akshay"
}
```

---

Orders Collection:

```json
{
  "userId": 1,
  "product": "Laptop",
  "price": 50000
}
```

---

## Fetch User Orders

```js
db.orders.find({ userId: 1 })
```

---

## Using Aggregation ($lookup)

```js
db.users.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "userId",
      as: "orders"
    }
  }
])
```

---

## User Roles (Authorization)

```json
{
  "name": "Akshay",
  "role": "admin"
}
```

---

## Common Roles

- user
- admin
- moderator

---

## Validation

```js
if (!email || !password) {
  throw new Error("Invalid data");
}
```

---

## Security Best Practices

- Hash passwords
- Use JWT for authentication
- Validate input
- Use HTTPS

---

## Pagination (Users List)

```js
db.users.find().skip(0).limit(10)
```

---

## Real World Example

```js
const users = db.collection("users");

await users.insertOne({
  name: "Akshay",
  email: "akshay@email.com",
  password: "hashed",
  isActive: true,
  createdAt: new Date()
});
```

---

## Scaling Considerations

- Index email
- Use pagination
- Avoid large documents
- Separate collections (users, orders)

---

## Summary

- Store user data securely
- Use indexes
- Use referencing for relationships
- Implement authentication properly
- Design for scalability