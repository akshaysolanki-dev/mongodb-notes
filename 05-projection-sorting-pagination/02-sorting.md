# 05-projection-sorting-pagination/02-sorting.md

# Sorting (Deep)

## Introduction

Sorting is used to arrange documents in a specific order.

MongoDB allows sorting:
- Ascending (low → high)
- Descending (high → low)

---

## Syntax

```js
db.collection.find().sort({ field: order })
```

- order = 1 → ascending
- order = -1 → descending

---

## Basic Sorting

### Ascending Order

```js
db.users.find().sort({ age: 1 })
```

---

### Descending Order

```js
db.users.find().sort({ age: -1 })
```

---

## Sorting by Multiple Fields

### Syntax

```js
db.collection.find().sort({
  field1: 1,
  field2: -1
})
```

---

### Example

```js
db.users.find().sort({
  age: 1,
  name: -1
})
```

Explanation:
- First sort by age (ascending)
- If same age → sort by name (descending)

---

## Sorting with Query

```js
db.users.find({ age: { $gt: 20 } }).sort({ age: -1 })
```

---

## Sorting with Projection

```js
db.users.find(
  {},
  { name: 1, age: 1 }
).sort({ age: 1 })
```

---

## Sorting Nested Fields

```js
db.users.find().sort({ "address.city": 1 })
```

---

## Sorting Arrays (Important Behavior)

MongoDB sorts based on:
- First element of array

Example:

```js
db.users.find().sort({ scores: 1 })
```

---

## Sorting with Limit

```js
db.users.find().sort({ age: -1 }).limit(5)
```

---

## Sorting with Skip

```js
db.users.find().sort({ age: 1 }).skip(5)
```

---

## Important Notes

- Sorting without index is slow
- Sorting large data consumes memory
- MongoDB may use disk if data is large

---

## Index and Sorting

If index exists on field:
- Sorting becomes very fast

Example:

```js
db.users.createIndex({ age: 1 })
```

---

## Common Mistakes

### Sorting Without Limit

```js
db.users.find().sort({ age: -1 })
```

⚠️ May return huge data

---

## Performance Tips

- Always combine sort with limit
- Use indexes on sorted fields
- Avoid sorting large collections without index

---

## Real World Example

```js
db.products.find(
  { category: "Electronics" }
).sort({ price: -1 }).limit(10)
```

---

## Summary

- 1 → ascending
- -1 → descending
- Can sort multiple fields
- Index improves sorting performance
- Combine with limit for efficiency