# 02-setup/03-compass-guide.md

# MongoDB Compass (GUI Guide)

## Introduction

MongoDB Compass is a graphical user interface (GUI) for MongoDB.

It allows you to:
- Visualize databases and collections
- Insert, update, and delete documents
- Run queries without using command line
- Analyze performance and indexes

---

## Installation

1. Download MongoDB Compass from official website
2. Install the application
3. Open MongoDB Compass

---

## Connecting to Database

### Default Connection

Use connection string:

```
mongodb://127.0.0.1:27017
```

Steps:
1. Open Compass
2. Paste connection string
3. Click "Connect"

---

## Interface Overview

### Left Panel

- Shows list of databases
- Expand database to view collections

---

### Main Panel

- Displays documents inside a collection
- Allows filtering, sorting, and editing

---

## Creating Database

1. Click "Create Database"
2. Enter:
   - Database name
   - Collection name
3. Click "Create"

---

## Creating Collection

1. Select database
2. Click "Create Collection"
3. Enter collection name

---

## Insert Document

1. Open collection
2. Click "Insert Document"
3. Add JSON data

Example:

```json
{
  "name": "Akshay",
  "age": 25
}
```

4. Click "Insert"

---

## Query (Filter Data)

Use filter bar:

```json
{ "age": { "$gt": 20 } }
```

---

## Edit Document

1. Click document
2. Modify fields
3. Click "Update"

---

## Delete Document

1. Click delete icon
2. Confirm deletion

---

## Sorting

Use sort option:

```json
{ "age": 1 }
```

- 1 → ascending
- -1 → descending

---

## Index Management

1. Go to "Indexes" tab
2. Click "Create Index"
3. Select field

---

## Aggregation Pipeline

1. Go to "Aggregation" tab
2. Add stages like:
   - $match
   - $group
   - $project

---

## Schema Tab

- Shows structure of documents
- Helps analyze fields and data types

---

## Performance Tab

- Shows query performance
- Helps optimize queries

---

## Advantages of Compass

- Easy to use
- No need to remember commands
- Visual debugging
- Good for beginners

---

## When to Use Compass

- Exploring data
- Debugging queries
- Learning MongoDB

---

## When NOT to Use

- Automation scripts
- Production backend logic

---

## Summary

MongoDB Compass is a powerful GUI tool that simplifies database interaction and helps visualize data effectively.