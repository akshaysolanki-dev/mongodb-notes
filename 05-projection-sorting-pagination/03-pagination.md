# 05-projection-sorting-pagination/03-pagination.md

# Pagination (Deep)

## Introduction

Pagination is used to divide large datasets into smaller chunks (pages).

It is important for:
- Performance
- User experience
- Efficient data loading

---

## Why Pagination is Needed

Without pagination:
- All data is loaded at once
- Slow performance
- High memory usage

With pagination:
- Load only required data
- Faster response

---

## Basic Pagination (skip + limit)

### Syntax

```js
db.collection.find().skip(n).limit(m)
```

- skip(n) → skip n documents
- limit(m) → return m documents

---

## Example

```js
db.users.find().skip(0).limit(5)
```

Page 1 → first 5 documents

---

## Page-wise Example

### Page 1

```js
db.users.find().skip(0).limit(5)
```

---

### Page 2

```js
db.users.find().skip(5).limit(5)
```

---

### Page 3

```js
db.users.find().skip(10).limit(5)
```

---

## Formula

```js
skip = (page - 1) * limit
```

---

### Example

Page = 3  
Limit = 5  

```js
skip = (3 - 1) * 5 = 10
```

---

## Pagination with Sorting

```js
db.users.find()
  .sort({ age: 1 })
  .skip(5)
  .limit(5)
```

---

## Pagination with Filter

```js
db.users.find({ age: { $gt: 20 } })
  .skip(5)
  .limit(5)
```

---

## Total Count

```js
db.users.countDocuments()
```

---

## Backend Pagination Example (Node.js)

```js
const page = 2;
const limit = 5;

const data = await db.collection("users")
  .find()
  .skip((page - 1) * limit)
  .limit(limit)
  .toArray();
```

---

## Problems with skip()

- Slow for large data
- MongoDB still scans skipped documents

---

## Better Approach (Range-based Pagination)

Use _id or indexed field.

---

### Example

```js
db.users.find({ _id: { $gt: lastId } }).limit(5)
```

---

### Advantages

- Faster
- Scales better
- Used in production systems

---

## Cursor-based Pagination (Concept)

Instead of page number:
- Use last document value

Example:
- lastId
- lastCreatedAt

---

## Important Notes

- Always use sort with pagination
- Avoid large skip values
- Prefer indexed fields

---

## Performance Tips

- Use indexes
- Avoid skip for large datasets
- Use cursor-based pagination

---

## Real World Example

```js
db.products.find({ category: "Electronics" })
  .sort({ price: -1 })
  .skip(10)
  .limit(10)
```

---

## Summary

- skip + limit → basic pagination
- skip formula → (page - 1) * limit
- Better approach → range-based pagination
- Always use sorting