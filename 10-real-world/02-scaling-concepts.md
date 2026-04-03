# 10-real-world/02-scaling-concepts.md

# Scaling Concepts in MongoDB (Deep)

## Introduction

Scaling is the ability of a system to handle increased load.

MongoDB supports:
- Vertical scaling
- Horizontal scaling (Sharding)
- Replication

---

## Types of Scaling

### 1. Vertical Scaling

Increase resources of a single server:
- CPU
- RAM
- Storage

---

### Advantages

- Simple to implement
- No architecture change

---

### Disadvantages

- Limited by hardware
- Expensive
- Single point of failure

---

## 2. Horizontal Scaling (Sharding)

### Definition

Distributing data across multiple servers.

---

## Sharding Concept

Data is split into smaller chunks and stored across shards.

---

## Components of Sharding

### 1. Shard

- Stores actual data
- Multiple shards in system

---

### 2. Config Server

- Stores metadata
- Keeps track of data distribution

---

### 3. Query Router (mongos)

- Routes queries to correct shard

---

## Shard Key (Very Important)

Determines how data is distributed.

---

### Example

```js
{ userId: 1 }
```

---

## Good Shard Key

- High cardinality
- Even distribution
- Frequently used in queries

---

## Bad Shard Key

- Low cardinality (e.g., gender)
- Causes uneven data distribution

---

## Example

```js
sh.shardCollection("db.users", { userId: 1 })
```

---

## Replication (Replica Set)

### Definition

Maintains multiple copies of data.

---

### Structure

- Primary → handles writes
- Secondary → copies data

---

## Failover

If primary fails:
- Secondary becomes primary automatically

---

## Advantages

- High availability
- Data redundancy
- Fault tolerance

---

## Read Scaling

Reads can be performed from:
- Primary
- Secondary (optional)

---

## Write Scaling

Writes only go to:
- Primary node

---

## Combined Scaling

MongoDB supports:
- Sharding + Replication

This provides:
- High performance
- High availability

---

## Load Balancing

MongoDB automatically distributes data across shards.

---

## Performance Tips

- Choose shard key carefully
- Use indexes
- Monitor query performance

---

## When to Scale

- Large dataset
- High traffic
- Performance issues

---

## Real World Example

Large e-commerce app:
- Users → sharded by userId
- Orders → sharded by orderId
- Replica sets for reliability

---

## Summary

- Vertical scaling → increase server power
- Horizontal scaling → distribute data
- Replication → ensure availability
- Sharding → key for large systems