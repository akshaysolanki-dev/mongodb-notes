# 04-query-deep-dive/05-evaluation-operators.md

# Evaluation Operators (Deep)

## Introduction

Evaluation operators are used for advanced querying.

They allow:
- Regular expression matching
- Conditional logic
- Expression-based filtering
- JavaScript execution (limited use)

---

## List of Evaluation Operators

- $regex
- $expr
- $mod
- $text
- $where (not recommended)

---

## $regex

### Definition

Used for pattern matching (like search).

---

### Syntax

```js
db.collection.find({
  field: { $regex: pattern, $options: "i" }
})
```

---

### Example (Starts With)

```js
db.users.find({
  name: { $regex: "^A" }
})
```

---

### Example (Contains)

```js
db.users.find({
  name: { $regex: "shay" }
})
```

---

### Case Insensitive

```js
db.users.find({
  name: { $regex: "akshay", $options: "i" }
})
```

---

## $expr

### Definition

Allows use of aggregation expressions inside queries.

---

### Example

```js
db.users.find({
  $expr: { $gt: ["$age", 25] }
})
```

---

### Compare Two Fields

```js
db.users.find({
  $expr: { $gt: ["$salary", "$expenses"] }
})
```

---

## $mod

### Definition

Matches values divisible by a number.

---

### Syntax

```js
db.collection.find({
  field: { $mod: [divisor, remainder] }
})
```

---

### Example

```js
db.users.find({
  age: { $mod: [5, 0] }
})
```

---

## $text

### Definition

Performs text search on indexed fields.

---

### Create Text Index

```js
db.users.createIndex({ name: "text" })
```

---

### Example

```js
db.users.find({
  $text: { $search: "Akshay" }
})
```

---

## $where (Not Recommended)

### Definition

Executes JavaScript inside query.

---

### Example

```js
db.users.find({
  $where: function () {
    return this.age > 25;
  }
})
```

---

### Warning

- Very slow
- Security risks
- Avoid in production

---

## Combining Evaluation Operators

```js
db.users.find({
  name: { $regex: "^A", $options: "i" },
  age: { $gt: 20 }
})
```

---

## Important Notes

- $regex is widely used
- $expr is powerful for dynamic conditions
- $text requires index
- Avoid $where

---

## Performance Tips

- Use indexes with $text
- Avoid heavy regex patterns
- Do not use $where in production

---

## Real World Example

```js
db.products.find({
  name: { $regex: "phone", $options: "i" }
})
```

---

## Summary

- $regex → pattern search
- $expr → dynamic conditions
- $mod → divisibility check
- $text → full-text search
- $where → avoid (slow)