# 04-query-deep-dive/01-comparison-operators.md

# Comparison Operators (Deep)

## Introduction

Comparison operators are used to compare values in queries.

They are mainly used inside find() to filter documents.

---

## List of Comparison Operators

- $eq  → equal
- $ne  → not equal
- $gt  → greater than
- $gte → greater than or equal
- $lt  → less than
- $lte → less than or equal
- $in  → matches any value in array
- $nin → does not match any value in array

---

## $eq (Equal)

### Definition

Matches documents where value is equal to specified value.

---

### Example

```js
db.users.find({ age: { $eq: 25 } })
```

Shortcut:

```js
db.users.find({ age: 25 })
```

---

## $ne (Not Equal)

### Definition

Matches documents where value is NOT equal.

---

### Example

```js
db.users.find({ age: { $ne: 25 } })
```

---

## $gt (Greater Than)

```js
db.users.find({ age: { $gt: 20 } })
```

---

## $gte (Greater Than or Equal)

```js
db.users.find({ age: { $gte: 25 } })
```

---

## $lt (Less Than)

```js
db.users.find({ age: { $lt: 30 } })
```

---

## $lte (Less Than or Equal)

```js
db.users.find({ age: { $lte: 25 } })
```

---

## $in

### Definition

Matches any value from given array.

---

### Example

```js
db.users.find({ age: { $in: [20, 25, 30] } })
```

---

## $nin

### Definition

Matches values NOT in given array.

---

### Example

```js
db.users.find({ age: { $nin: [20, 25] } })
```

---

## Combining Multiple Conditions

```js
db.users.find({
  age: { $gt: 20, $lt: 30 }
})
```

---

## Comparison on Strings

```js
db.users.find({ name: { $eq: "Akshay" } })
```

---

## Comparison on Dates

```js
db.users.find({
  createdAt: { $gt: new Date("2024-01-01") }
})
```

---

## Comparison on Nested Fields

```js
db.users.find({
  "address.city": { $eq: "Delhi" }
})
```

---

## Comparison on Arrays

```js
db.users.find({
  skills: { $in: ["MongoDB"] }
})
```

---

## Important Notes

- Operators start with $
- Can combine multiple operators
- Works with numbers, strings, dates

---

## Performance Tips

- Use indexes on fields used in comparison
- Avoid unnecessary conditions
- Combine conditions smartly

---

## Real World Example

```js
db.products.find({
  price: { $gte: 10000, $lte: 50000 }
})
```

---

## Summary

Comparison operators help filter data based on values.

Most used:
- $gt, $lt → ranges
- $in → multiple values
- $ne → exclusions