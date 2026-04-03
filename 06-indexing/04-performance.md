# 06-indexing/04-performance.md

# Indexing Performance (Deep)

## Introduction

Indexes improve read performance but affect write performance.

Understanding trade-offs is important for production systems.

---

## How Index Improves Performance

Without index:
- MongoDB performs COLLSCAN (collection scan)
- Checks every document

With index:
- MongoDB performs IXSCAN (index scan)
- Directly finds matching documents

---

## Read vs Write Trade-off

### Read Operations

- Faster with index
- Efficient filtering and sorting

---

### Write Operations

- Slower with index
- Every insert/update must update index

---

## Example

```js
db.users.insertOne({ name: "Akshay", age: 25 })
```

If indexes exist on:
- name
- age

MongoDB must update:
- Document
- Index for name
- Index for age

---

## Memory Usage

Indexes consume RAM.

If too many indexes:
- Memory usage increases
- Performance may degrade

---

## Disk Usage

Indexes also take disk space.

Large collections → large indexes

---

## Explain Method (Very Important)

### Syntax

```js
db.collection.find(query).explain("executionStats")
```

---

### Example

```js
db.users.find({ age: 25 }).explain("executionStats")
```

---

### Key Output Fields

- stage: COLLSCAN or IXSCAN
- nReturned: number of documents returned
- totalDocsExamined: documents scanned
- totalKeysExamined: index entries scanned

---

## Covered Query

### Definition

Query uses only indexed fields → no need to fetch full document

---

### Example

```js
db.users.createIndex({ name: 1, age: 1 })

db.users.find(
  { name: "Akshay" },
  { name: 1, age: 1, _id: 0 }
)
```

---

## Index Selectivity

### Definition

Selectivity = how unique values are

---

### Example

Field with high selectivity:
- email (unique)

Field with low selectivity:
- gender (few values)

---

### Rule

- High selectivity → better index performance

---

## Index Intersection

MongoDB can combine multiple indexes.

---

### Example

```js
db.users.createIndex({ name: 1 })
db.users.createIndex({ age: 1 })

db.users.find({ name: "Akshay", age: 25 })
```

---

## When Index is NOT Used

- Small collections
- Query not matching index
- Using wrong field order
- Low selectivity

---

## Over-Indexing Problem

Too many indexes:
- Slower writes
- Increased memory usage
- Complex maintenance

---

## Best Practices

- Index frequently queried fields
- Avoid indexing every field
- Use compound indexes wisely
- Monitor using explain()

---

## Performance Tips

- Use covered queries
- Avoid unnecessary projections
- Use limit() with queries
- Combine index with sorting

---

## Real World Example

```js
db.products.createIndex({ category: 1, price: 1 })

db.products.find({
  category: "Electronics",
  price: { $gt: 10000 }
})
```

---

## Summary

- Index improves read performance
- Slows down writes
- Uses memory and disk
- Use explain() to analyze
- Balance is key