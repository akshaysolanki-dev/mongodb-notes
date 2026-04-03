# 01-fundamentals/01-what-is-mongodb.md

# What is MongoDB

## Definition

MongoDB is a NoSQL, document-oriented database that stores data in BSON (Binary JSON) format.

It is designed for:
- High performance
- Scalability
- Flexible schema

---

## Core Concept

MongoDB structure:

Database → Collection → Document

---

## Example Document

```json
{
  "_id": "1",
  "name": "Akshay",
  "age": 25,
  "skills": ["JavaScript", "MongoDB"]
}
```

---

## BSON (Binary JSON)

MongoDB stores data in BSON instead of JSON.

Advantages:
- Faster parsing
- Supports additional data types

Extra BSON data types:
- ObjectId
- Date
- Binary
- Decimal128

---

## Key Features

### 1. Flexible Schema

Documents in same collection can differ:

```json
{ "name": "Akshay" }
{ "name": "Rohit", "age": 25 }
```

### 2. Nested Data Support

```json
{
  "name": "Akshay",
  "address": {
    "city": "Delhi",
    "pin": 110001
  }
}
```

### 3. High Performance

- No joins (mostly)
- Index support
- Optimized read/write

### 4. Horizontal Scaling

Supports sharding:
- Distributes data across servers

---

## When to Use

- Dynamic schema
- REST APIs
- Real-time apps
- MERN stack

---

## When Not to Use

- Complex joins
- Strict relational data
- Banking-level transactions

---

## Summary

MongoDB is best suited for modern applications where flexibility and speed are required.