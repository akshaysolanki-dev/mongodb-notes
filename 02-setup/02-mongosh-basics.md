# 02-setup/02-mongosh-basics.md

# MongoDB Shell (mongosh) Basics

## Introduction

MongoDB Shell (mongosh) is the command-line interface used to interact with MongoDB.

It allows you to:
- Create databases
- Insert data
- Query data
- Update and delete data

---

## Start Mongo Shell

```bash
mongosh
```

---

## Default Connection

```bash
mongodb://127.0.0.1:27017
```

---

## Show Databases

```js
show dbs
```

---

## Create / Switch Database

```js
use myDatabase
```

- If database exists → switches
- If not → created on first insert

---

## Check Current Database

```js
db
```

---

## Show Collections

```js
show collections
```

---

## Create Collection

```js
db.createCollection("users")
```

---

## Insert Data

```js
db.users.insertOne({ name: "Akshay", age: 25 })
```

---

## Find Data

```js
db.users.find()
```

---

## Pretty Output

```js
db.users.find().pretty()
```

---

## Find One Document

```js
db.users.findOne({ name: "Akshay" })
```

---

## Update Data

```js
db.users.updateOne(
  { name: "Akshay" },
  { $set: { age: 26 } }
)
```

---

## Delete Data

```js
db.users.deleteOne({ name: "Akshay" })
```

---

## Drop Collection

```js
db.users.drop()
```

---

## Drop Database

```js
db.dropDatabase()
```

---

## Help Commands

```js
help
db.help()
db.users.help()
```

---

## Clear Screen

```js
cls
```

---

## Exit Shell

```js
exit
```

---

## JavaScript Support

mongosh supports JavaScript:

```js
for (let i = 1; i <= 5; i++) {
  db.test.insertOne({ number: i })
}
```

---

## Variables

```js
let user = { name: "Akshay", age: 25 }
db.users.insertOne(user)
```

---

## Important Notes

- mongosh uses JavaScript syntax
- Commands are case-sensitive
- Collections are created automatically

---

## Summary

mongosh is used to:
- Interact with MongoDB
- Run queries
- Manage data

It is essential for practice and backend development.