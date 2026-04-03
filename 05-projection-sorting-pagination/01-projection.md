# 05-projection-sorting-pagination/01-projection.md

# Projection (Deep)

## Introduction

Projection is used to control which fields are returned in query results.

By default:
- MongoDB returns all fields

Projection helps:
- Reduce data transfer
- Improve performance
- Return only required data

---

## Syntax

```js
db.collection.find(query, projection)
```

---

## Include Fields

### Example

```js
db.users.find({}, { name: 1, age: 1 })
```

---

### Output

```json
{
  "_id": ObjectId("..."),
  "name": "Akshay",
  "age": 25
}
```

---

## Exclude Fields

### Example

```js
db.users.find({}, { age: 0 })
```

---

## Remove _id Field

```js
db.users.find({}, { _id: 0, name: 1 })
```

---

## Rules of Projection

- Cannot mix include (1) and exclude (0)
- Exception: _id can be excluded with include

---

## Projection with Nested Fields

```js
db.users.find({}, { "address.city": 1 })
```

---

## Projection with Arrays

```js
db.users.find({}, { skills: 1 })
```

---

## Project Specific Array Element

```js
db.users.find({}, { "skills.0": 1 })
```

---

## Using $slice (Array Projection)

### Definition

Limits number of array elements returned

---

### Example

```js
db.users.find({}, { skills: { $slice: 2 } })
```

---

### Last Elements

```js
db.users.find({}, { skills: { $slice: -2 } })
```

---

## Projection with $elemMatch

```js
db.users.find(
  {},
  {
    scores: { $elemMatch: { $gt: 80 } }
  }
)
```

---

## Why Projection is Important

- Reduces response size
- Faster queries
- Improves backend performance

---

## Common Mistakes

### Mixing Include and Exclude

```js
db.users.find({}, { name: 1, age: 0 })
```

❌ Invalid

---

## Performance Tips

- Always fetch only required fields
- Avoid large unnecessary data transfer
- Combine with indexing

---

## Real World Example

```js
db.products.find(
  { price: { $gt: 10000 } },
  { name: 1, price: 1, _id: 0 }
)
```

---

## Summary

- Projection controls output fields
- 1 → include field
- 0 → exclude field
- Cannot mix include and exclude (except _id)
- Improves performance