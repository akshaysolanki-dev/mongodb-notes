# 01-fundamentals/03-nosql-vs-sql-deep.md

# NoSQL vs SQL (Deep Comparison)

## Introduction

Databases are broadly divided into two categories:

1. SQL (Relational Databases)
2. NoSQL (Non-Relational Databases)

MongoDB is a NoSQL database.

---

## Data Structure

### SQL (Relational)

- Data stored in tables
- Fixed rows and columns
- Schema must be defined before inserting data

Example:

| id | name   | age |
|----|--------|-----|
| 1  | Akshay | 25  |

---

### MongoDB (NoSQL)

- Data stored in documents
- JSON-like structure (BSON)
- Flexible schema

Example:

```json
{
  "_id": 1,
  "name": "Akshay",
  "age": 25
}
```

---

## Schema

### SQL

- Strict schema
- All rows must follow same structure
- Changing schema is difficult

### MongoDB

- Dynamic schema
- Documents in same collection can differ

```json
{ "name": "Akshay" }
{ "name": "Rohit", "age": 25 }
```

---

## Relationships

### SQL

- Uses JOIN operations
- Data is normalized (split across tables)

Example:

```sql
SELECT users.name, orders.item
FROM users
JOIN orders ON users.id = orders.user_id;
```

---

### MongoDB

- Avoids joins
- Uses:
  - Embedded documents
  - Referencing (manual linking)

Example (Embedded):

```json
{
  "name": "Akshay",
  "orders": [
    { "item": "Laptop", "price": 50000 }
  ]
}
```

---

## Scalability

### SQL

- Vertical scaling
- Increase CPU/RAM of single server

Limit:
- Hardware dependent

---

### MongoDB

- Horizontal scaling
- Data distributed across multiple servers (Sharding)

Advantage:
- Can handle very large datasets

---

## Performance

### SQL

- Slower for complex joins
- Strong consistency

### MongoDB

- Faster reads/writes
- No joins improves performance

---

## Transactions

### SQL

- Strong ACID properties
- Used in banking systems

ACID:
- Atomicity
- Consistency
- Isolation
- Durability

---

### MongoDB

- Supports transactions (multi-document)
- But generally optimized for performance over strict ACID

---

## Query Language

### SQL

```sql
SELECT * FROM users WHERE age > 25;
```

---

### MongoDB

```js
db.users.find({ age: { $gt: 25 } })
```

---

## Flexibility

### SQL

- Rigid structure
- Not suitable for rapidly changing data

### MongoDB

- Highly flexible
- Easy to modify structure anytime

---

## Use Cases

### SQL Best For

- Banking systems
- Financial applications
- Complex relational data

---

### MongoDB Best For

- Real-time apps
- Social media platforms
- E-commerce
- REST APIs
- MERN stack apps

---

## Advantages of MongoDB over SQL

- Flexible schema
- Better performance (in many cases)
- Easy scaling
- Developer-friendly (JSON)

---

## Disadvantages of MongoDB

- Not ideal for complex joins
- Less strict data integrity
- Can lead to inconsistent data if not designed properly

---

## Summary

| Feature        | SQL                  | MongoDB             |
|----------------|----------------------|---------------------|
| Structure      | Tables               | Collections         |
| Schema         | Fixed                | Flexible            |
| Relationships  | JOINs                | Embedded/Reference  |
| Scaling        | Vertical             | Horizontal          |
| Performance    | Slower with joins    | Faster (no joins)   |
| Transactions   | Strong ACID          | Limited ACID        |

---

## Final Conclusion

Choose SQL when:
- Data is structured
- Relationships are complex
- Strong consistency required

Choose MongoDB when:
- Data is flexible
- High performance needed
- Application needs scalability