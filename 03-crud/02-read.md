# 03-crud/02-read.md

# READ Operations (Deep)

## Introduction

READ operations are used to retrieve data from MongoDB.

Main methods:
- find()
- findOne()

---

## find()

### Definition

Returns all documents that match a query.

---

### Syntax

```js
db.collection.find(query, projection)
```

- query → filter condition
- projection → fields to return

---

### Get All Documents

```js
db.users.find()
```

---

### Pretty Format

```js
db.users.find().pretty()
```

---

## findOne()

### Definition

Returns the first matching document.

---

### Syntax

```js
db.collection.findOne(query)
```

---

### Example

```js
db.users.findOne({ name: "Akshay" })
```

---

## Filtering (Query)

### Exact Match

```js
db.users.find({ age: 25 })
```

---

### Multiple Conditions (AND)

```js
db.users.find({
  age: 25,
  name: "Akshay"
})
```

---

## Comparison Operators

### Greater Than

```js
db.users.find({ age: { $gt: 20 } })
```

---

### Less Than

```js
db.users.find({ age: { $lt: 30 } })
```

---

### Greater Than or Equal

```js
db.users.find({ age: { $gte: 25 } })
```

---

### Less Than or Equal

```js
db.users.find({ age: { $lte: 25 } })
```

---

### Not Equal

```js
db.users.find({ age: { $ne: 25 } })
```

---

### In Operator

```js
db.users.find({ age: { $in: [20, 25] } })
```

---

## Logical Operators

### OR

```js
db.users.find({
  $or: [
    { age: { $lt: 20 } },
    { age: { $gt: 30 } }
  ]
})
```

---

### AND

```js
db.users.find({
  $and: [
    { age: 25 },
    { name: "Akshay" }
  ]
})
```

---

### NOT

```js
db.users.find({
  age: { $not: { $gt: 25 } }
})
```

---

## Projection (Selecting Fields)

### Include Fields

```js
db.users.find({}, { name: 1, age: 1 })
```

---

### Exclude Fields

```js
db.users.find({}, { age: 0 })
```

---

### Rules

- Cannot mix include and exclude (except _id)
- _id is included by default

---

### Remove _id

```js
db.users.find({}, { _id: 0, name: 1 })
```

---

## Sorting

### Ascending

```js
db.users.find().sort({ age: 1 })
```

---

### Descending

```js
db.users.find().sort({ age: -1 })
```

---

## Limit

```js
db.users.find().limit(2)
```

---

## Skip

```js
db.users.find().skip(2)
```

---

## Pagination Example

```js
db.users.find().skip(10).limit(5)
```

---

## Count Documents

```js
db.users.countDocuments()
```

---

## Find by _id

```js
db.users.find({ _id: ObjectId("507f1f77bcf86cd799439011") })
```

---

## Nested Field Query

```js
db.users.find({ "address.city": "Delhi" })
```

---

## Array Query

### Match Element

```js
db.users.find({ skills: "MongoDB" })
```

---

### Using $all

```js
db.users.find({ skills: { $all: ["JS", "MongoDB"] } })
```

---

## Cursor (Important)

find() returns a cursor.

Convert to array:

```js
db.users.find().toArray()
```

---

## Performance Tips

- Use indexes for faster queries
- Avoid fetching unnecessary fields
- Use limit for large datasets

---

## Real World Example

```js
db.products.find(
  { price: { $gt: 10000 } },
  { name: 1, price: 1 }
).sort({ price: -1 }).limit(5)
```

---

## Summary

- find() → multiple documents
- findOne() → single document
- Supports filtering, sorting, pagination
- Uses powerful query operators