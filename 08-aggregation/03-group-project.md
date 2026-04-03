# 08-aggregation/03-group-project.md

# $group and $project (Deep)

## Introduction

Two of the most important aggregation stages:

- $group → used for grouping and calculations
- $project → used for shaping and transforming data

---

## $group (Deep)

### Definition

Groups documents by a specified field and performs calculations.

---

## Syntax

```js
{
  $group: {
    _id: <group_by_field>,
    fieldName: { operator: <expression> }
  }
}
```

---

## Basic Example

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId"
    }
  }
])
```

---

## Group with Sum

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

## Group with Count

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      totalOrders: { $sum: 1 }
    }
  }
])
```

---

## Group with Average

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      avgAmount: { $avg: "$amount" }
    }
  }
])
```

---

## Group with Min and Max

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      minAmount: { $min: "$amount" },
      maxAmount: { $max: "$amount" }
    }
  }
])
```

---

## Group with $push (Array)

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      orders: { $push: "$amount" }
    }
  }
])
```

---

## Group by Multiple Fields

```js
db.orders.aggregate([
  {
    $group: {
      _id: {
        user: "$userId",
        status: "$status"
      },
      total: { $sum: "$amount" }
    }
  }
])
```

---

## $project (Deep)

### Definition

Used to:
- Include/exclude fields
- Create new fields
- Transform data

---

## Basic Example

```js
db.users.aggregate([
  {
    $project: {
      name: 1,
      age: 1
    }
  }
])
```

---

## Remove _id

```js
db.users.aggregate([
  {
    $project: {
      _id: 0,
      name: 1
    }
  }
])
```

---

## Create New Field

```js
db.users.aggregate([
  {
    $project: {
      name: 1,
      isAdult: { $gte: ["$age", 18] }
    }
  }
])
```

---

## Rename Field

```js
db.users.aggregate([
  {
    $project: {
      userName: "$name"
    }
  }
])
```

---

## Math Operations

```js
db.orders.aggregate([
  {
    $project: {
      totalWithTax: { $multiply: ["$amount", 1.18] }
    }
  }
])
```

---

## Combine $group and $project

```js
db.orders.aggregate([
  {
    $group: {
      _id: "$userId",
      total: { $sum: "$amount" }
    }
  },
  {
    $project: {
      _id: 0,
      userId: "$_id",
      total: 1
    }
  }
])
```

---

## Important Notes

- $group changes structure completely
- $project controls final output
- _id is required in $group

---

## Performance Tips

- Use $match before $group
- Keep $project minimal
- Avoid unnecessary fields

---

## Real World Example

```js
db.sales.aggregate([
  { $match: { status: "completed" } },
  {
    $group: {
      _id: "$productId",
      totalSales: { $sum: "$amount" }
    }
  },
  {
    $project: {
      productId: "$_id",
      totalSales: 1,
      _id: 0
    }
  }
])
```

---

## Summary

- $group → grouping + calculations
- $project → shaping output
- Used together for powerful data transformation