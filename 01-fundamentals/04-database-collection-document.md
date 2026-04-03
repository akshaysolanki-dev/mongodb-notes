# 01-fundamentals/04-database-collection-document.md

# Database, Collection, Document (Deep Understanding)

## Introduction

MongoDB organizes data in a hierarchical structure:

Database → Collection → Document → Field

Understanding this hierarchy is critical for designing efficient databases.

---

## Database

### Definition

A database is a container for collections.

It is the top-level structure in MongoDB.

---

### Create / Switch Database

```js
use myDatabase
```

- If database exists → switches to it
- If not → creates it (when data is inserted)

---

### Show Databases

```js
show dbs
```

---

### Current Database

```js
db
```

---

## Collection

### Definition

A collection is a group of documents.

Equivalent to a "table" in SQL, but without fixed schema.

---

### Create Collection

```js
db.createCollection("users")
```

---

### Auto Creation

MongoDB automatically creates collection when inserting data:

```js
db.users.insertOne({ name: "Akshay" })
```

---

### Show Collections

```js
show collections
```

---

## Document

### Definition

A document is a single record stored in a collection.

It is stored in BSON format.

---

### Example

```json
{
  "name": "Akshay",
  "age": 25,
  "skills": ["JavaScript", "MongoDB"]
}
```

---

### Rules of Document

- Must be valid JSON-like structure
- Field names are strings
- Values can be different data types
- Documents can have different structure

---

## Field

### Definition

A field is a key-value pair inside a document.

Example:

```json
{
  "name": "Akshay"
}
```

- "name" → field
- "Akshay" → value

---

## _id Field (Very Important)

### Definition

Every document must have a unique `_id` field.

MongoDB automatically generates it if not provided.

---

### Example

```json
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "Akshay"
}
```

---

### Properties

- Unique
- Indexed by default
- Used for fast lookup

---

## Data Types in MongoDB

### Common Types

- String
- Number (int, double)
- Boolean
- Array
- Object
- Date
- Null

---

### Example

```json
{
  "name": "Akshay",
  "age": 25,
  "isActive": true,
  "skills": ["JS", "MongoDB"],
  "createdAt": new Date()
}
```

---

## Nested Documents

MongoDB allows storing objects inside objects.

```json
{
  "name": "Akshay",
  "address": {
    "city": "Delhi",
    "pincode": 110001
  }
}
```

---

## Arrays

MongoDB supports arrays.

```json
{
  "skills": ["JavaScript", "Node.js", "MongoDB"]
}
```

---

## Why This Structure Matters

- Flexible schema
- Easy to store complex data
- Reduces need for joins

---

## Real World Example

User document:

```json
{
  "name": "Akshay",
  "email": "akshay@email.com",
  "orders": [
    { "item": "Laptop", "price": 50000 },
    { "item": "Mouse", "price": 500 }
  ]
}
```

---

## Summary

- Database → contains collections
- Collection → contains documents
- Document → actual data
- Field → key-value pair

MongoDB’s power comes from flexible documents and nested structures.