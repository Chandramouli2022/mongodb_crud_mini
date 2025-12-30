Below are the **most frequently used MongoDB operations** you’ll use in **real projects & interviews**, grouped cleanly and kept **concise** (as you prefer).

Examples shown in **MongoDB shell syntax**, with **Mongoose equivalents** where useful.

---

## 1️⃣ Database & Collection

```js
use mydb
show dbs
show collections
```

---

## 2️⃣ Insert Operations

### Insert One

```js
db.users.insertOne({ name: "John", age: 25 })
```

**Mongoose**

```js
User.create({ name: "John", age: 25 });
```

### Insert Many

```js
db.users.insertMany([
  { name: "A", age: 20 },
  { name: "B", age: 30 }
])
```

---

## 3️⃣ Read (Find) Operations

### Find All

```js
db.users.find()
```

### Find with Condition

```js
db.users.find({ age: { $gt: 25 } })
```

### Find One

```js
db.users.findOne({ email: "a@test.com" })
```

### Find by ID

```js
db.users.find({ _id: ObjectId("64f...") })
```

**Mongoose**

```js
User.findById(id);
```

---

## 4️⃣ Projection (Select Fields)

```js
db.users.find({}, { name: 1, email: 1, _id: 0 })
```

**Mongoose**

```js
User.find().select("name email");
```

---

## 5️⃣ Update Operations

### Update One

```js
db.users.updateOne(
  { email: "a@test.com" },
  { $set: { age: 28 } }
)
```

### Update Many

```js
db.users.updateMany(
  { age: { $lt: 18 } },
  { $set: { minor: true } }
)
```

### Increment Field

```js
db.users.updateOne(
  { _id: id },
  { $inc: { loginCount: 1 } }
)
```

**Mongoose**

```js
User.findByIdAndUpdate(id, { age: 28 }, { new: true });
```

---

## 6️⃣ Delete Operations

### Delete One

```js
db.users.deleteOne({ email: "a@test.com" })
```

### Delete Many

```js
db.users.deleteMany({ inactive: true })
```

**Mongoose**

```js
User.findByIdAndDelete(id);
```

---

## 7️⃣ Sorting, Limiting, Pagination

```js
db.users.find().sort({ age: -1 }).limit(5).skip(10)
```

**Mongoose**

```js
User.find().sort({ age: -1 }).limit(5).skip(10);
```

---

## 8️⃣ Count Documents

```js
db.users.countDocuments({ age: { $gt: 25 } })
```

---

## 9️⃣ Indexing (Very Important)

### Create Index

```js
db.users.createIndex({ email: 1 }, { unique: true })
```

### List Indexes

```js
db.users.getIndexes()
```

---

## 🔟 Aggregation (Very Common in Production)

### Group & Count

```js
db.users.aggregate([
  { $group: { _id: "$age", count: { $sum: 1 } } }
])
```

### Filter + Group

```js
db.users.aggregate([
  { $match: { age: { $gt: 18 } } },
  { $group: { _id: null, avgAge: { $avg: "$age" } } }
])
```

**Mongoose**

```js
User.aggregate([
  { $match: { age: { $gt: 18 } } },
  { $group: { _id: null, avgAge: { $avg: "$age" } } }
]);
```

---

## 1️⃣1️⃣ Operators You Must Know

| Operator       | Usage             |
| -------------- | ----------------- |
| `$gt`, `$lt`   | Greater / Less    |
| `$gte`, `$lte` | >= / <=           |
| `$in`          | Match array       |
| `$ne`          | Not equal         |
| `$or`, `$and`  | Logical           |
| `$set`         | Update field      |
| `$inc`         | Increment         |
| `$push`        | Add to array      |
| `$pull`        | Remove from array |

Example:

```js
db.users.find({
  $or: [{ age: { $gt: 30 } }, { role: "admin" }]
})
```

---

## 1️⃣2️⃣ Transactions (Advanced but Common)

```js
session.startTransaction();
```

Used in **banking / payments / critical flows**.

---

## Interview Tip (Important)

If asked:

> **“What MongoDB operations do you use most?”**

Answer:

> “Primarily `find`, `findOne`, `updateOne`, `updateMany`, `aggregate`, indexing, pagination with `skip & limit`, and atomic operators like `$set` and `$inc`.”

---

If you want:

* **Real-world aggregation examples**
* **Performance optimization tips**
* **MongoDB vs SQL comparison**
* **Production pitfalls**

Just say 👍
