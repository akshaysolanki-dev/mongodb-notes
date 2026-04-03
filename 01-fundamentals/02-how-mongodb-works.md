# 01-fundamentals/02-how-mongodb-works.md

# How MongoDB Works (Deep Explanation)

## Storage Engine

MongoDB uses the WiredTiger storage engine by default.

Responsibilities of storage engine:
- Manages how data is stored on disk
- Handles compression
- Controls concurrency
- Manages memory usage

---

## Data Storage

MongoDB stores data in BSON format inside collections.

- Each collection is stored as files on disk
- Documents are grouped inside collections
- Data is not stored in rows like SQL

---

## Memory Usage (Important)

MongoDB uses RAM for performance optimization.

### Working Set

Working set = Frequently accessed data kept in memory

If working set fits in RAM:
- Queries are very fast

If not:
- MongoDB reads from disk (slower)

---

## Indexing Mechanism

Indexes store data in sorted order.

Without index:
- MongoDB scans entire collection (slow)

With index:
- Direct lookup (fast)

Example:
```js
db.users.createIndex({ name: 1 })
```

---

## Write Operation Flow

When you insert/update data:

1. Request comes to MongoDB server
2. Data is written to memory
3. Journal logs the operation
4. Data is written to disk

---

## Journaling (Crash Safety)

MongoDB maintains a journal file.

Purpose:
- Prevent data loss
- Recover data after crash

If system crashes:
- MongoDB replays journal logs

---

## Read Operation Flow

1. Query received
2. MongoDB checks for index
3. If index exists → fast lookup
4. Data fetched from:
   - RAM (fast)
   - Disk (slower)

---

## Concurrency Control

MongoDB uses document-level locking.

Meaning:
- Multiple users can access database simultaneously
- Only one operation locks a document at a time

---

## Replication (High Availability)

MongoDB uses Replica Sets.

Structure:
- Primary → handles writes
- Secondary → copies data

If primary fails:
- Secondary becomes primary automatically

---

## Sharding (Scaling)

Used for very large applications.

Concept:
- Data is distributed across multiple servers

Shard Key:
- Determines how data is split

---

## Summary

MongoDB internally works using:
- WiredTiger storage engine
- Memory caching (working set)
- Indexing system
- Journaling for safety
- Replication for availability
- Sharding for scalability