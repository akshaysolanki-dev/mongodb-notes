# 07-schema-design/01-embedding-vs-referencing.md

# Embedding vs Referencing (Deep)

## Introduction

In MongoDB, relationships between data can be handled in two ways:

1. Embedding (Nested Documents)
2. Referencing (Linking Documents)

Choosing the right approach is critical for performance and scalability.

---

## Embedding

### Definition

Embedding means storing related data inside the same document.

---

### Example

```json
{
  "name": "Akshay",
  "orders": [
    { "item": "Laptop", "price": 50000 },
    { "item": "Mouse", "price": 500 }
  ]
}
```

---

## Advantages of Embedding

- Faster reads (no joins required)
- Data is stored together
- Fewer queries needed
- Atomic updates possible

---

## Disadvantages of Embedding

- Document size can grow large
- Data duplication possible
- Difficult to update nested large data

---

## When to Use Embedding

- One-to-few relationships
- Data accessed together
- Small datasets

---

## Referencing

### Definition

Referencing means storing a reference (usually _id) to another document.

---

### Example

#### Users Collection

```json
{
  "_id": 1,
  "name": "Akshay"
}
```

---

#### Orders Collection

```json
{
  "userId": 1,
  "item": "Laptop",
  "price": 50000
}
```

---

## Advantages of Referencing

- Avoids data duplication
- Better for large datasets
- Easier to update data
- Scales well

---

## Disadvantages of Referencing

- Requires multiple queries
- No native joins (manual or aggregation)
- Slower reads compared to embedding

---

## When to Use Referencing

- One-to-many (large data)
- Many-to-many relationships
- Frequently updated data

---

## Comparison Table

| Feature        | Embedding             | Referencing           |
|----------------|----------------------|-----------------------|
| Read Speed     | Fast                 | Slower                |
| Write Speed    | Fast                 | Moderate              |
| Data Duplication | Possible           | Minimal               |
| Scalability    | Limited              | High                  |
| Complexity     | Simple               | Complex               |

---

## Hybrid Approach

Sometimes both are used.

Example:
- Embed small data
- Reference large data

---

## Real World Example

### E-commerce

- User + few recent orders → Embed
- Full order history → Reference

---

## Best Practices

- Keep documents under 16MB
- Avoid deeply nested structures
- Choose based on query patterns

---

## Key Rule

"Design schema based on how data is read, not how it is stored."

---

## Summary

- Embedding → fast reads, simple data
- Referencing → scalable, large data
- Choose based on use case