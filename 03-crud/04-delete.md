# 03-crud/04-delete.md

# DELETE Operations (Deep)

## Introduction

DELETE operations are used to remove documents from a MongoDB collection.

Main methods:
- deleteOne()
- deleteMany()

---

## deleteOne()

### Definition

Deletes the first document that matches the filter.

---

### Syntax

```js
db.collection.deleteOne(filter)
```

---

### Example

```js
db.users.deleteOne({ name: "Akshay" })
```

---

### Output

```json
{
  "acknowledged": true,
  "deletedCount": 1
}
```

---

## deleteMany()

### Definition

Deletes all documents that match the filter.

---

### Syntax

```js
db.collection.deleteMany(filter)
```

---

### Example

```js
db.users.deleteMany({ age: { $lt: 18 } })
```

---

### Output

```json
{
  "acknowledged": true,
  "deletedCount": 5
}
```

---

## Delete All Documents

```js
db.users.deleteMany({})
```

⚠️ Warning:
- Deletes all documents in collection
- Collection still exists

---

## Drop Collection

### Definition

Removes entire collection (including all documents and indexes)

---

### Syntax

```js
db.users.drop()
```

---

## Drop Database

### Definition

Deletes entire database

---

### Syntax

```js
db.dropDatabase()
```

---

## Delete with Condition

```js
db.users.deleteMany({
  status: "inactive"
})
```

---

## Delete Using Operators

```js
db.users.deleteMany({
  age: { $gt: 60 }
})
```

---

## Delete Nested Field Condition

```js
db.users.deleteMany({
  "address.city": "Delhi"
})
```

---

## Delete Array Match

```js
db.users.deleteMany({
  skills: "MongoDB"
})
```

---

## Important Notes

- deleteOne → deletes only first match
- deleteMany → deletes all matches
- Filters are very important

---

## Common Mistakes

### Missing Filter

```js
db.users.deleteMany()
```

⚠️ Error: filter required

---

### Empty Filter

```js
db.users.deleteMany({})
```

⚠️ Deletes everything

---

## Soft Delete (Best Practice)

Instead of deleting:

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { isDeleted: true } }
)
```

---

## Why Soft Delete?

- Data recovery possible
- Audit logs maintained

---

## Performance Tips

- Use indexes on filter fields
- Avoid deleting large data at once
- Use batching for large deletes

---

## Real World Example

```js
db.orders.deleteMany({
  status: "cancelled"
})
```

---

## Summary

- deleteOne → removes one document
- deleteMany → removes multiple documents
- drop → removes collection
- dropDatabase → removes database
- Always use filters carefully