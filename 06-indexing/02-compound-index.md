# 06-indexing/02-compound-index.md

# Compound Index (Deep)

## Introduction

A compound index is an index on multiple fields.

It is used when queries involve more than one field.

---

## Syntax

```js
db.collection.createIndex({ field1: 1, field2: 1 })
```

---

## Example

```js
db.users.createIndex({ age: 1, name: 1 })
```

---

## How Compound Index Works

MongoDB stores index in sorted order based on fields.

Order matters.

Example index:

```js
{ age: 1, name: 1 }
```

Sorting order:
1. First by age
2. Then by name

---

## Query Usage

### Works

```js
db.users.find({ age: 25, name: "Akshay" })
```

---

### Works (Prefix Rule)

```js
db.users.find({ age: 25 })
```

---

### Does NOT Work Efficiently

```js
db.users.find({ name: "Akshay" })
```

---

## Prefix Rule (Very Important)

A compound index can be used only if query includes the first field(s).

Example:

Index:
```js
{ age: 1, name: 1 }
```

Valid queries:
- { age }
- { age, name }

Invalid:
- { name } ❌

---

## Sorting with Compound Index

```js
db.users.find().sort({ age: 1, name: 1 })
```

Uses index efficiently.

---

## Mixed Order Index

```js
db.users.createIndex({ age: 1, name: -1 })
```

---

## Example Use Case

```js
db.orders.createIndex({ userId: 1, createdAt: -1 })
```

Used for:
- Fetching user orders
- Sorted by latest first

---

## Covered Queries (Important)

If query uses only indexed fields:
- MongoDB does not fetch full document

Example:

```js
db.users.createIndex({ name: 1, age: 1 })

db.users.find(
  { name: "Akshay" },
  { name: 1, age: 1, _id: 0 }
)
```

---

## Limitations

- Order matters
- Too many fields → large index size
- Not useful if query pattern is different

---

## Best Practices

- Put most frequently queried field first
- Use for multi-field queries
- Avoid unnecessary fields

---

## Performance Tips

- Follow prefix rule
- Combine with sorting
- Use explain() to verify

---

## Real World Example

```js
db.products.createIndex({ category: 1, price: -1 })
```

---

## Summary

- Compound index → multiple fields
- Order matters
- Prefix rule is critical
- Improves performance for complex queries