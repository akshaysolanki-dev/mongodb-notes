# 03-crud/03-update.md

# UPDATE Operations (Deep)

## Introduction

UPDATE operations are used to modify existing documents in MongoDB.

Main methods:
- updateOne()
- updateMany()
- replaceOne()

---

## updateOne()

### Definition

Updates the first document that matches the filter.

---

### Syntax

```js
db.collection.updateOne(filter, update, options)
```

---

### Example

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { age: 26 } }
)
```

---

### Output

```json
{
  "acknowledged": true,
  "matchedCount": 1,
  "modifiedCount": 1
}
```

---

## updateMany()

### Definition

Updates all documents that match the filter.

---

### Syntax

```js
db.collection.updateMany(filter, update, options)
```

---

### Example

```js
db.users.updateMany(
  { age: { $gt: 20 } },
  { $set: { status: "active" } }
)
```

---

## replaceOne()

### Definition

Replaces the entire document.

---

### Syntax

```js
db.collection.replaceOne(filter, newDocument)
```

---

### Example

```js
db.users.replaceOne(
  { name: "Akshay" },
  { name: "Akshay", age: 30 }
)
```

⚠️ Note:
- Old document is completely replaced
- Fields not included will be removed

---

## Update Operators (Very Important)

### $set

Adds or updates fields

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { city: "Delhi" } }
)
```

---

### $inc

Increments numeric value

```js
db.users.updateOne(
  { name: "Akshay" },
  { $inc: { age: 1 } }
)
```

---

### $unset

Removes a field

```js
db.users.updateOne(
  { name: "Akshay" },
  { $unset: { age: "" } }
)
```

---

### $rename

Renames a field

```js
db.users.updateOne(
  { name: "Akshay" },
  { $rename: { "name": "fullName" } }
)
```

---

## Array Update Operators

### $push

Adds value to array

```js
db.users.updateOne(
  { name: "Akshay" },
  { $push: { skills: "Node.js" } }
)
```

---

### $pull

Removes value from array

```js
db.users.updateOne(
  { name: "Akshay" },
  { $pull: { skills: "JS" } }
)
```

---

### $addToSet

Adds only if not exists

```js
db.users.updateOne(
  { name: "Akshay" },
  { $addToSet: { skills: "MongoDB" } }
)
```

---

## Upsert Option

### Definition

If document does not exist → insert new document

---

### Example

```js
db.users.updateOne(
  { name: "Unknown" },
  { $set: { age: 20 } },
  { upsert: true }
)
```

---

## Update Nested Fields

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { "address.city": "Delhi" } }
)
```

---

## Update Multiple Fields

```js
db.users.updateOne(
  { name: "Akshay" },
  {
    $set: {
      age: 26,
      city: "Delhi"
    }
  }
)
```

---

## Common Mistakes

### Missing $set

```js
db.users.updateOne(
  { name: "Akshay" },
  { age: 30 }
)
```

⚠️ This replaces entire document

---

### Correct Way

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { age: 30 } }
)
```

---

## Performance Tips

- Use updateMany carefully
- Use indexes on filter fields
- Avoid large document rewrites

---

## Real World Example

```js
db.products.updateMany(
  { category: "Electronics" },
  { $inc: { stock: 5 } }
)
```

---

## Summary

- updateOne → updates one document
- updateMany → updates multiple documents
- replaceOne → replaces entire document
- Use operators like $set, $inc, $push
- Upsert creates document if not found