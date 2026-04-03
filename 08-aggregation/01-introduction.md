# 08-aggregation/01-introduction.md

# Aggregation (Deep)

## Introduction

Aggregation is used to process and transform data in MongoDB.

It allows:
- Filtering
- Grouping
- Calculating
- Reshaping data

Similar to SQL:
- GROUP BY
- SUM
- COUNT

---

## Aggregation Pipeline

MongoDB uses a pipeline approach.

Data flows through stages step-by-step.

---

## Syntax

```js
db.collection.aggregate([
  { stage1 },
  { stage2 },
  { stage3 }
])
```

---

## Example

```js
db.users.aggregate([
  { $match: { age: { $gt: 20 } } },
  { $project: { name: 1, age: 1 } }
])
```

---

## How Pipeline Works

1. Input documents
2. Stage 1 processes data
3. Output goes to next stage
4. Final result returned

---

## Common Use Cases

- Data analysis
- Reports
- Dashboard metrics
- Grouping data

---

## Important Stages (Overview)

- $match → filter data
- $group → group data
- $project → select/transform fields
- $sort → sort results
- $limit → limit results
- $skip → skip documents

---

## Example (Group Data)

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      total: { $sum: "$amount" }
    }
  }
])
```

---

## Example (Filter + Group)

```js
db.orders.aggregate([
  { $match: { amount: { $gt: 100 } } },
  {
    $group: {
      _id: "$userId",
      total: { $sum: "$amount" }
    }
  }
])
```

---

## Example (Project Fields)

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

## Difference from find()

find():
- Simple queries
- No transformation

aggregate():
- Complex processing
- Data transformation

---

## Important Notes

- Order of stages matters
- Early filtering improves performance
- Use indexes with $match

---

## Performance Tips

- Use $match early
- Limit data as soon as possible
- Avoid unnecessary stages

---

## Real World Example

```js
db.products.aggregate([
  { $match: { category: "Electronics" } },
  { $sort: { price: -1 } },
  { $limit: 5 }
])
```

---

## Summary

- Aggregation = data processing pipeline
- Uses multiple stages
- Powerful for analytics and transformations