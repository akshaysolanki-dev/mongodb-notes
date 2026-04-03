# 08-aggregation/02-pipeline-stages.md

# Aggregation Pipeline Stages (Deep)

## Introduction

Aggregation pipeline consists of multiple stages.

Each stage performs a specific operation on data.

---

## Common Pipeline Stages

- $match
- $project
- $group
- $sort
- $limit
- $skip
- $unwind
- $lookup

---

## $match

### Definition

Filters documents (like find).

---

### Example

```js
db.users.aggregate([
  { $match: { age: { $gt: 20 } } }
])
```

---

### Best Practice

- Use $match early for performance

---

## $project

### Definition

Selects and transforms fields.

---

### Example

```js
db.users.aggregate([
  {
    $project: {
      name: 1,
      age: 1,
      isAdult: { $gte: ["$age", 18] }
    }
  }
])
```

---

## $group

### Definition

Groups documents by a field and performs calculations.

---

### Example

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      totalAmount: { $sum: "$amount" }
    }
  }
])
```

---

### Common Operators

- $sum
- $avg
- $min
- $max
- $push

---

## $sort

### Definition

Sorts documents.

---

### Example

```js
db.users.aggregate([
  { $sort: { age: -1 } }
])
```

---

## $limit

### Definition

Limits number of documents.

---

### Example

```js
db.users.aggregate([
  { $limit: 5 }
])
```

---

## $skip

### Definition

Skips documents.

---

### Example

```js
db.users.aggregate([
  { $skip: 5 }
])
```

---

## $unwind

### Definition

Deconstructs array into multiple documents.

---

### Example

```js
db.users.aggregate([
  { $unwind: "$skills" }
])
```

---

### Input

```json
{
  "name": "Akshay",
  "skills": ["JS", "MongoDB"]
}
```

---

### Output

```json
{ "name": "Akshay", "skills": "JS" }
{ "name": "Akshay", "skills": "MongoDB" }
```

---

## $lookup

### Definition

Performs join with another collection.

---

### Syntax

```js
{
  $lookup: {
    from: "collection",
    localField: "field",
    foreignField: "field",
    as: "result"
  }
}
```

---

### Example

```js
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "userDetails"
    }
  }
])
```

---

## Combining Stages

```js
db.orders.aggregate([
  { $match: { amount: { $gt: 100 } } },
  {
    $group: {
      _id: "$userId",
      total: { $sum: "$amount" }
    }
  },
  { $sort: { total: -1 } }
])
```

---

## Important Notes

- Order of stages matters
- $match first → better performance
- $group is expensive operation

---

## Performance Tips

- Filter early
- Limit data
- Avoid unnecessary stages
- Use indexes with $match

---

## Real World Example

```js
db.products.aggregate([
  { $match: { category: "Electronics" } },
  { $unwind: "$tags" },
  { $group: { _id: "$tags", count: { $sum: 1 } } }
])
```

---

## Summary

- Pipeline = multiple stages
- Each stage transforms data
- Most used: $match, $group, $project
- Powerful for complex queries