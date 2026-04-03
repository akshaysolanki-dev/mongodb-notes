# 07-schema-design/02-schema-patterns.md

# Schema Design Patterns (Deep)

## Introduction

Schema design patterns are commonly used structures to solve real-world problems in MongoDB.

They help in:
- Improving performance
- Reducing complexity
- Scaling applications

---

## 1. Attribute Pattern

### Problem

Documents have many optional fields.

---

### Solution

Store dynamic fields inside a single object.

---

### Example

```json
{
  "name": "Laptop",
  "attributes": {
    "color": "black",
    "ram": "16GB",
    "storage": "512GB"
  }
}
```

---

### Use Case

- E-commerce products
- Dynamic properties

---

## 2. Bucket Pattern

### Problem

Large number of small documents (e.g., logs, time-series data)

---

### Solution

Group data into buckets.

---

### Example

```json
{
  "userId": 1,
  "logs": [
    { "time": "10:00", "action": "login" },
    { "time": "10:05", "action": "view" }
  ]
}
```

---

### Use Case

- IoT data
- Analytics
- Logs

---

## 3. Subset Pattern

### Problem

Large document but only small part is frequently accessed

---

### Solution

Split into:
- Frequently used data
- Rarely used data

---

### Example

```json
{
  "name": "Akshay",
  "profile": { "bio": "..." },
  "settings": { "theme": "dark" }
}
```

---

### Use Case

- User profiles
- Dashboards

---

## 4. Extended Reference Pattern

### Problem

Referencing requires multiple queries

---

### Solution

Store some duplicated fields for faster reads

---

### Example

```json
{
  "userId": 1,
  "userName": "Akshay"
}
```

---

### Use Case

- Frequently accessed related data

---

## 5. Computed Pattern

### Problem

Repeated calculations slow down queries

---

### Solution

Store computed values

---

### Example

```json
{
  "totalOrders": 25
}
```

---

### Use Case

- Dashboards
- Reports

---

## 6. Polymorphic Pattern

### Problem

Different document structures in same collection

---

### Solution

Allow flexible schema

---

### Example

```json
{ "type": "user", "name": "Akshay" }
{ "type": "admin", "permissions": ["all"] }
```

---

### Use Case

- Multiple entity types

---

## 7. Tree Pattern

### Problem

Hierarchical data (categories)

---

### Solution

Store parent-child relationship

---

### Example

```json
{
  "name": "Electronics",
  "parent": null
}
```

---

## 8. Outlier Pattern

### Problem

Few documents are very large

---

### Solution

Separate large data

---

### Example

```json
{
  "name": "Akshay",
  "hasExtraData": true
}
```

---

## Best Practices

- Design based on query patterns
- Avoid deep nesting
- Balance read vs write performance
- Use indexing with patterns

---

## Real World Example

E-commerce:
- Products → Attribute pattern
- Orders → Reference pattern
- Analytics → Bucket pattern

---

## Summary

Schema patterns help:
- Optimize performance
- Handle real-world data
- Build scalable systems