# 04-query-deep-dive/03-element-operators.md

# Element Operators (Deep)

## Introduction

Element operators are used to check:
- Existence of fields
- Data types of fields

They are useful when dealing with flexible schema.

---

## List of Element Operators

- $exists
- $type

---

## $exists

### Definition

Checks whether a field exists in a document.

---

### Syntax

```js
db.collection.find({
  field: { $exists: true/false }
})
```

---

### Example (Field Exists)

```js
db.users.find({
  age: { $exists: true }
})
```

---

### Example (Field Does Not Exist)

```js
db.users.find({
  age: { $exists: false }
})
```

---

### Use Case

When documents have different structures:

```json
{ "name": "Akshay" }
{ "name": "Rohit", "age": 25 }
```

Find only documents with age:

```js
db.users.find({
  age: { $exists: true }
})
```

---

## $type

### Definition

Matches documents where field is of a specific data type.

---

### Syntax

```js
db.collection.find({
  field: { $type: <type> }
})
```

---

### Example (String Type)

```js
db.users.find({
  name: { $type: "string" }
})
```

---

### Example (Number Type)

```js
db.users.find({
  age: { $type: "int" }
})
```

---

### Common BSON Types

| Type        | Value       |
|-------------|------------|
| String      | "string"   |
| Integer     | "int"      |
| Double      | "double"   |
| Boolean     | "bool"     |
| Array       | "array"    |
| Object      | "object"   |
| Date        | "date"     |
| ObjectId    | "objectId" |

---

### Example with Date

```js
db.users.find({
  createdAt: { $type: "date" }
})
```

---

## Combining $exists and $type

```js
db.users.find({
  age: { $exists: true, $type: "int" }
})
```

---

## Nested Field Check

```js
db.users.find({
  "address.city": { $exists: true }
})
```

---

## Use Cases

- Handling optional fields
- Validating schema-like structure
- Cleaning inconsistent data

---

## Important Notes

- MongoDB allows flexible schema
- Not all documents have same fields
- These operators help manage that

---

## Performance Tips

- Use indexes when possible
- Avoid unnecessary checks on large collections

---

## Real World Example

```js
db.products.find({
  discount: { $exists: true }
})
```

---

## Summary

Element operators help in:

- Checking field existence → $exists
- Checking data type → $type

Useful in flexible schema environments