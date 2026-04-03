# 06-indexing/01-index-basics.md

# Index Basics (Deep)

## Introduction

Indexes are used to improve query performance in MongoDB.

Without index:
- MongoDB scans entire collection (COLLSCAN)

With index:
- MongoDB uses fast lookup (IXSCAN)

---

## What is an Index

An index is a data structure that stores field values in sorted order.

It allows MongoDB to:
- Quickly locate documents
- Avoid scanning entire collection

---

## Default Index

MongoDB automatically creates an index on:

```js
_id
```

This index is:
- Unique
- Fast
- Always present

---

## Create Index

### Syntax

```js
db.collection.createIndex({ field: 1 })
```

---

### Example

```js
db.users.createIndex({ age: 1 })
```

---

## Index Order

- 1 → ascending
- -1 → descending

---

### Example

```js
db.users.createIndex({ age: -1 })
```

---

## How Index Works

Without index:

```js
db.users.find({ age: 25 })
```

MongoDB:
- Checks every document

---

With index:

- Uses index to directly find matching documents

---

## Check Indexes

```js
db.users.getIndexes()
```

---

## Drop Index

```js
db.users.dropIndex({ age: 1 })
```

---

## Unique Index

### Definition

Ensures values are unique

---

### Example

```js
db.users.createIndex({ email: 1 }, { unique: true })
```

---

## Partial Index (Concept)

Index only specific documents

---

### Example

```js
db.users.createIndex(
  { age: 1 },
  { partialFilterExpression: { age: { $gt: 18 } } }
)
```

---

## Sparse Index

Only indexes documents where field exists

---

### Example

```js
db.users.createIndex({ age: 1 }, { sparse: true })
```

---

## Explain Query (Important)

```js
db.users.find({ age: 25 }).explain("executionStats")
```

---

### Output Insight

- COLLSCAN → no index
- IXSCAN → index used

---

## Index Impact

### Advantages

- Faster queries
- Efficient searching

---

### Disadvantages

- Uses extra memory
- Slows down writes (insert/update)

---

## When to Use Index

- Frequently queried fields
- Sorting fields
- Filtering conditions

---

## When NOT to Use

- Small collections
- Rarely queried fields
- Too many indexes

---

## Performance Tips

- Create index on filter fields
- Avoid unnecessary indexes
- Monitor using explain()

---

## Real World Example

```js
db.products.createIndex({ price: 1 })
```

---

## Summary

- Index improves read performance
- Default index on _id
- Use createIndex()
- Check with explain()
- Balance between read and write performance