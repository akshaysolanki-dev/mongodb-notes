# 02-setup/01-installation.md

# MongoDB Installation (Complete Guide)

## Introduction

To start using MongoDB, you need to install:

1. MongoDB Server (Database)
2. MongoDB Shell (CLI tool)
3. MongoDB Compass (GUI tool)

---

## MongoDB Components

### 1. MongoDB Server

- Core database system
- Runs in background
- Handles data storage and queries

---

### 2. MongoDB Shell (mongosh)

- Command Line Interface (CLI)
- Used to interact with database using commands

---

### 3. MongoDB Compass

- Graphical User Interface (GUI)
- Helps visualize databases, collections, and documents

---

## Installation Steps (Windows)

### Step 1: Download MongoDB

- Go to official MongoDB website
- Download MongoDB Community Server

---

### Step 2: Install MongoDB

- Run installer
- Choose "Complete Setup"
- Install MongoDB as a service

---

### Step 3: Install MongoDB Shell

- Download mongosh separately (if not included)
- Add to system PATH

---

### Step 4: Install MongoDB Compass

- Download MongoDB Compass
- Install it

---

## Verify Installation

### Check MongoDB Server

```bash
mongod --version
```

---

### Check MongoDB Shell

```bash
mongosh --version
```

---

## Start MongoDB

### If installed as service (Windows)

MongoDB starts automatically

---

### Manual Start (if needed)

```bash
mongod
```

---

## Connect to MongoDB

```bash
mongosh
```

---

## Default Connection

MongoDB runs on:

```
mongodb://127.0.0.1:27017
```

---

## Common Issues

### 1. mongosh not recognized

Solution:
- Add MongoDB bin folder to PATH

---

### 2. Connection failed

Check:
- MongoDB service is running

---

### 3. Port already in use

- Change port or stop conflicting service

---

## Folder Structure (Internal)

MongoDB stores data in:

```
C:\Program Files\MongoDB\Server\<version>\data\
```

---

## Best Practices

- Always run MongoDB as service
- Use Compass for visualization
- Use mongosh for practice

---

## Summary

To start MongoDB:

1. Install MongoDB Server
2. Install mongosh
3. Install Compass
4. Run mongosh to connect