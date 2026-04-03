# 03-crud/01-create.md

# CREATE Operations (Deep)

## Introduction

CREATE operations are used to insert data into a MongoDB collection.

MongoDB provides:
- insertOne()
- insertMany()

---

## insertOne()

### Definition

Inserts a single document into a collection.

---

### Syntax

```js
db.collection.insertOne(document)
```

---

### Example

```js
db.users.insertOne({
  name: "Akshay",
  age: 25,
  isActive: true
})
```

---

### Output

```json
{
  "acknowledged": true,
  "insertedId": ObjectId("...")
}
```

---

### Important Points

- If collection does not exist → it is created automatically
- If `_id` is not provided → MongoDB generates it

---

## insertMany()

### Definition

Inserts multiple documents at once.

---

### Syntax

```js
db.collection.insertMany([doc1, doc2, ...])
```

---

### Example

```js
db.users.insertMany([
  { name: "A", age: 20 },
  { name: "B", age: 30 },
  { name: "C", age: 40 }
])
```

---

### Output

```json
{
  "acknowledged": true,
  "insertedIds": {
    "0": ObjectId("..."),
    "1": ObjectId("..."),
    "2": ObjectId("...")
  }
}
```

---

## Ordered vs Unordered Inserts

### Ordered (default)

- Inserts documents one by one
- Stops if error occurs

```js
db.users.insertMany(docs, { ordered: true })
```

---

### Unordered

- Inserts all documents
- Continues even if some fail

```js
db.users.insertMany(docs, { ordered: false })
```

---

## _id Field (Important)

### Auto Generated

```json
{
  "_id": ObjectId("507f1f77bcf86cd799439011")
}
```

---

### Custom _id

```js
db.users.insertOne({
  _id: 1,
  name: "Akshay"
})
```

---

### Rules

- Must be unique
- Cannot be duplicated

---

## Data Types in Insert

### Example

```js
db.users.insertOne({
  name: "Akshay",
  age: 25,
  isActive: true,
  skills: ["JS", "MongoDB"],
  address: {
    city: "Delhi"
  },
  createdAt: new Date()
})
```

---

## Insert Nested Documents

```js
db.users.insertOne({
  name: "Akshay",
  orders: [
    { item: "Laptop", price: 50000 },
    { item: "Mouse", price: 500 }
  ]
})
```

---

## Insert with Validation (Concept)

MongoDB can enforce schema validation (advanced).

Example (concept):

```js
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name"],
      properties: {
        name: {
          bsonType: "string"
        }
      }
    }
  }
})
```

---

## Common Errors

### Duplicate _id

```js
E11000 duplicate key error
```

---

### Invalid Data Type

- Wrong structure
- Missing required fields (if validation enabled)

---

## Performance Tips

- Use insertMany for bulk inserts
- Avoid inserting one by one in loops
- Use indexes carefully

---

## Real World Example

```js
db.products.insertMany([
  {
    name: "Laptop",
    price: 50000,
    category: "Electronics",
    stock: 10
  },
  {
    name: "Phone",
    price: 20000,
    category: "Electronics",
    stock: 25
  }
])
```

---

## Summary

- insertOne → single document
- insertMany → multiple documents
- _id → unique identifier
- Supports nested and flexible data