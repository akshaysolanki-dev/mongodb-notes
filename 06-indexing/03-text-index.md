# 06-indexing/03-text-index.md

# Text Index (Deep)

## Introduction

Text index is used for full-text search in MongoDB.

It allows searching:
- Words
- Phrases
- Text content

---

## Why Text Index

Normal queries:
- Match exact values

Text index:
- Supports search like:
  - Contains word
  - Multiple words
  - Relevance-based results

---

## Create Text Index

### Syntax

```js
db.collection.createIndex({ field: "text" })
```

---

### Example

```js
db.users.createIndex({ name: "text" })
```

---

## Multiple Fields Text Index

```js
db.users.createIndex({
  name: "text",
  description: "text"
})
```

---

## Search Using $text

### Syntax

```js
db.collection.find({
  $text: { $search: "keyword" }
})
```

---

### Example

```js
db.users.find({
  $text: { $search: "Akshay" }
})
```

---

## Search Multiple Words

```js
db.users.find({
  $text: { $search: "Akshay developer" }
})
```

---

## Exact Phrase Search

```js
db.users.find({
  $text: { $search: "\"Akshay Solanki\"" }
})
```

---

## Exclude Word

```js
db.users.find({
  $text: { $search: "Akshay -developer" }
})
```

---

## Text Score (Relevance)

### Definition

MongoDB assigns score based on relevance.

---

### Example

```js
db.users.find(
  { $text: { $search: "Akshay" } },
  { score: { $meta: "textScore" } }
).sort({ score: { $meta: "textScore" } })
```

---

## Weights (Important)

Give importance to specific fields.

---

### Example

```js
db.users.createIndex(
  {
    name: "text",
    description: "text"
  },
  {
    weights: {
      name: 5,
      description: 1
    }
  }
)
```

---

## Language Support

MongoDB supports language-specific stemming.

---

### Example

```js
db.users.createIndex(
  { description: "text" },
  { default_language: "english" }
)
```

---

## Limitations

- Only one text index per collection
- Cannot combine with other index types
- Not suitable for complex search engines

---

## Performance Notes

- Faster than regex for text search
- Requires index creation
- Large text fields may impact performance

---

## When to Use

- Search functionality
- Blog/article search
- Product search

---

## When NOT to Use

- Advanced search engines
- Complex ranking systems

---

## Real World Example

```js
db.products.createIndex({
  name: "text",
  description: "text"
})

db.products.find({
  $text: { $search: "laptop gaming" }
})
```

---

## Summary

- Text index → full-text search
- Uses $text operator
- Supports phrases and multiple words
- Provides relevance scoring