# 04-query-deep-dive/02-logical-operators.md

# Logical Operators (Deep)

## Introduction

Logical operators are used to combine multiple query conditions.

They help create complex queries using:
- AND
- OR
- NOT
- NOR

---

## List of Logical Operators

- $and
- $or
- $not
- $nor

---

## $and

### Definition

Matches documents that satisfy ALL conditions.

---

### Syntax

```js
db.collection.find({
  $and: [
    { condition1 },
    { condition2 }
  ]
})
```

---

### Example

```js
db.users.find({
  $and: [
    { age: { $gt: 20 } },
    { age: { $lt: 30 } }
  ]
})
```

---

### Shortcut (Implicit AND)

```js
db.users.find({
  age: { $gt: 20, $lt: 30 }
})
```

---

## $or

### Definition

Matches documents that satisfy ANY condition.

---

### Syntax

```js
db.collection.find({
  $or: [
    { condition1 },
    { condition2 }
  ]
})
```

---

### Example

```js
db.users.find({
  $or: [
    { age: { $lt: 20 } },
    { age: { $gt: 30 } }
  ]
})
```

---

## $not

### Definition

Negates a condition.

---

### Syntax

```js
db.collection.find({
  field: { $not: { condition } }
})
```

---

### Example

```js
db.users.find({
  age: { $not: { $gt: 25 } }
})
```

---

## $nor

### Definition

Matches documents that do NOT satisfy ANY condition.

---

### Syntax

```js
db.collection.find({
  $nor: [
    { condition1 },
    { condition2 }
  ]
})
```

---

### Example

```js
db.users.find({
  $nor: [
    { age: { $lt: 20 } },
    { age: { $gt: 30 } }
  ]
})
```

---

## Combining Logical Operators

```js
db.users.find({
  $and: [
    { age: { $gt: 20 } },
    {
      $or: [
        { name: "Akshay" },
        { name: "Rohit" }
      ]
    }
  ]
})
```

---

## Logical Operators with Nested Fields

```js
db.users.find({
  $or: [
    { "address.city": "Delhi" },
    { "address.city": "Mumbai" }
  ]
})
```

---

## Logical Operators with Arrays

```js
db.users.find({
  $and: [
    { skills: "MongoDB" },
    { skills: "Node.js" }
  ]
})
```

---

## Important Notes

- $and is implicit in most cases
- $or is heavily used in filtering
- $not works on single condition
- $nor is opposite of $or

---

## Performance Tips

- Use indexes for fields used in conditions
- Avoid too many nested conditions
- Keep queries simple when possible

---

## Real World Example

```js
db.products.find({
  $or: [
    { price: { $lt: 10000 } },
    { category: "Electronics" }
  ]
})
```

---

## Summary

Logical operators combine multiple conditions:

- $and → all conditions true
- $or → any condition true
- $not → negate condition
- $nor → none of the conditions true