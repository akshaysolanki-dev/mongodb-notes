# 04-query-deep-dive/04-array-operators.md

# Array Operators (Deep)

## Introduction

Array operators are used to query documents that contain array fields.

They help in:
- Matching array values
- Checking conditions inside arrays
- Filtering based on array size or elements

---

## List of Array Operators

- $all
- $elemMatch
- $size

---

## Matching Array Values (Basic)

### Example

```js
db.users.find({ skills: "MongoDB" })
```

Matches documents where "MongoDB" exists inside skills array.

---

## $all

### Definition

Matches documents where array contains ALL specified elements.

---

### Syntax

```js
db.collection.find({
  field: { $all: [value1, value2] }
})
```

---

### Example

```js
db.users.find({
  skills: { $all: ["JS", "MongoDB"] }
})
```

---

## $elemMatch

### Definition

Matches documents where at least one array element satisfies multiple conditions.

---

### Syntax

```js
db.collection.find({
  arrayField: {
    $elemMatch: { condition }
  }
})
```

---

### Example

```js
db.users.find({
  scores: {
    $elemMatch: { $gt: 70, $lt: 90 }
  }
})
```

---

### Example (Objects in Array)

```js
db.orders.find({
  items: {
    $elemMatch: {
      price: { $gt: 1000 },
      quantity: { $gte: 2 }
    }
  }
})
```

---

## $size

### Definition

Matches arrays with exact number of elements.

---

### Syntax

```js
db.collection.find({
  field: { $size: number }
})
```

---

### Example

```js
db.users.find({
  skills: { $size: 3 }
})
```

---

## Query Nested Arrays

```js
db.users.find({
  "orders.item": "Laptop"
})
```

---

## Using $in with Arrays

```js
db.users.find({
  skills: { $in: ["MongoDB", "Node.js"] }
})
```

---

## Array Index Query

```js
db.users.find({
  "skills.0": "JavaScript"
})
```

---

## Important Notes

- MongoDB treats arrays as first-class data types
- Queries can match any element in array
- $elemMatch is important for multiple conditions

---

## Performance Tips

- Index array fields if frequently queried
- Avoid large arrays when possible
- Use $elemMatch instead of multiple conditions

---

## Real World Example

```js
db.products.find({
  tags: { $all: ["electronics", "sale"] }
})
```

---

## Summary

- Direct match → matches any element
- $all → all values must exist
- $elemMatch → multiple conditions on same element
- $size → exact array length