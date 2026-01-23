<div align="center">

# 💾 Chapter 07 · Data Management

### SQL · NoSQL · CRUD Operations

![Data Management](https://media.giphy.com/media/l46Cy1rHbQ92uuLXa/giphy.gif)

> *"Data is the new oil. But unlike oil, data gets more valuable when you refine it properly."*

[🔙 Back to Chapter 06](./06-web-dev-basics.md) • [Next Chapter 🔜](./08-backend-dev.md)

</div>

---

## 🗄️ Why Data Management Matters

Every application needs to:

- 💾 **Store** data persistently
- 🔍 **Retrieve** data efficiently
- ✏️ **Update** data accurately
- 🗑️ **Delete** data safely

Without proper data management:
- ❌ Your app loses information on restart
- ❌ Performance degrades as data grows
- ❌ Users can't trust your system
- ❌ Scaling becomes impossible

> 💡 **The database is often the bottleneck. Choose wisely.**

---

## 🎯 SQL vs NoSQL: The Great Divide

| Aspect | 🏛️ SQL (Relational) | 🌊 NoSQL (Non-Relational) |
|--------|---------------------|---------------------------|
| **Structure** | Tables with fixed schema | Flexible documents/collections |
| **Data Model** | Rows and columns | JSON-like documents, key-value, graphs |
| **Scaling** | Vertical (bigger servers) | Horizontal (more servers) |
| **Best For** | Complex queries, transactions | Fast reads/writes, flexible data |
| **Examples** | PostgreSQL, MySQL, SQLite | MongoDB, Redis, Cassandra |
| **When to Use** | Banking, e-commerce | Social media, real-time apps |

### 🧠 Mental Model

**SQL:**
> 📊 Like an Excel spreadsheet with strict rules

**NoSQL:**
> 📦 Like a flexible filing cabinet

---

## 🏛️ Part 1 · SQL Databases

### *Structured Query Language*

SQL databases organize data into **tables** with **relationships**.

### 📋 Basic Table Structure

```sql
Users Table:
┌────┬──────────┬─────────────────────┬─────┐
│ id │   name   │        email        │ age │
├────┼──────────┼─────────────────────┼─────┤
│ 1  │ Alice    │ alice@email.com     │ 28  │
│ 2  │ Bob      │ bob@email.com       │ 34  │
│ 3  │ Charlie  │ charlie@email.com   │ 22  │
└────┴──────────┴─────────────────────┴─────┘
```

### 🔧 Creating Tables

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    age INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 📊 Common Data Types

| Type | Description | Example |
|------|-------------|---------|
| `INTEGER` | Whole numbers | 42, -10, 0 |
| `TEXT` | Strings | "Hello", "user@email.com" |
| `REAL` | Decimals | 3.14, 99.99 |
| `BOOLEAN` | True/False | TRUE, FALSE |
| `DATE/TIMESTAMP` | Date and time | 2026-01-11 |

### 🔗 Relationships Between Tables

```sql
-- Users table
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

-- Posts table (related to users)
CREATE TABLE posts (
    id INTEGER PRIMARY KEY,
    user_id INTEGER,
    title TEXT,
    content TEXT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### 🧠 Types of Relationships

- **One-to-Many**: One user → many posts
- **Many-to-Many**: Many students ↔ many courses
- **One-to-One**: One user → one profile

---

## 📝 Part 2 · CRUD Operations

### *The Four Fundamental Actions*

**CRUD** = Create, Read, Update, Delete

Every database interaction falls into one of these categories.

### ✨ CREATE (Insert Data)

```sql
-- Insert a single user
INSERT INTO users (name, email, age)
VALUES ('Alice', 'alice@email.com', 28);

-- Insert multiple users
INSERT INTO users (name, email, age)
VALUES 
    ('Bob', 'bob@email.com', 34),
    ('Charlie', 'charlie@email.com', 22);
```

### 🔍 READ (Query Data)

```sql
-- Get all users
SELECT * FROM users;

-- Get specific columns
SELECT name, email FROM users;

-- Filter with WHERE
SELECT * FROM users WHERE age > 25;

-- Sort results
SELECT * FROM users ORDER BY age DESC;

-- Limit results
SELECT * FROM users LIMIT 10;

-- Count records
SELECT COUNT(*) FROM users;
```

### 🔧 Advanced Queries

```sql
-- Search with LIKE
SELECT * FROM users WHERE name LIKE 'A%';

-- Multiple conditions
SELECT * FROM users 
WHERE age > 20 AND age < 30;

-- Join tables
SELECT users.name, posts.title
FROM users
JOIN posts ON users.id = posts.user_id;

-- Group and aggregate
SELECT age, COUNT(*) as count
FROM users
GROUP BY age;
```

### ✏️ UPDATE (Modify Data)

```sql
-- Update a single record
UPDATE users
SET age = 29
WHERE id = 1;

-- Update multiple records
UPDATE users
SET age = age + 1
WHERE age < 30;

-- Update multiple columns
UPDATE users
SET name = 'Alice Smith', email = 'alice.smith@email.com'
WHERE id = 1;
```

### 🗑️ DELETE (Remove Data)

```sql
-- Delete specific record
DELETE FROM users WHERE id = 3;

-- Delete based on condition
DELETE FROM users WHERE age < 18;

-- Delete all records (dangerous!)
DELETE FROM users;

-- Better: Use soft deletes
UPDATE users SET deleted_at = CURRENT_TIMESTAMP WHERE id = 3;
```

---

## 🌊 Part 3 · NoSQL Databases

### *Flexibility Over Structure*

NoSQL databases use flexible, document-based storage.

### 📦 MongoDB Example

**Document Structure (JSON-like):**
```javascript
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "Alice",
  "email": "alice@email.com",
  "age": 28,
  "address": {
    "street": "123 Main St",
    "city": "New York"
  },
  "hobbies": ["reading", "coding", "hiking"],
  "created_at": "2026-01-11T10:30:00Z"
}
```

### ✨ CREATE (Insert Documents)

```javascript
// Insert one document
db.users.insertOne({
  name: "Alice",
  email: "alice@email.com",
  age: 28
});

// Insert multiple documents
db.users.insertMany([
  { name: "Bob", email: "bob@email.com", age: 34 },
  { name: "Charlie", email: "charlie@email.com", age: 22 }
]);
```

### 🔍 READ (Query Documents)

```javascript
// Find all documents
db.users.find();

// Find with filter
db.users.find({ age: { $gt: 25 } });

// Find one document
db.users.findOne({ email: "alice@email.com" });

// Select specific fields
db.users.find({}, { name: 1, email: 1 });

// Sort and limit
db.users.find().sort({ age: -1 }).limit(10);
```

### ✏️ UPDATE (Modify Documents)

```javascript
// Update one document
db.users.updateOne(
  { email: "alice@email.com" },
  { $set: { age: 29 } }
);

// Update multiple documents
db.users.updateMany(
  { age: { $lt: 30 } },
  { $inc: { age: 1 } }
);

// Add to array
db.users.updateOne(
  { name: "Alice" },
  { $push: { hobbies: "swimming" } }
);
```

### 🗑️ DELETE (Remove Documents)

```javascript
// Delete one document
db.users.deleteOne({ _id: ObjectId("507f1f77bcf86cd799439011") });

// Delete multiple documents
db.users.deleteMany({ age: { $lt: 18 } });
```

---

## 🎯 Part 4 · Choosing the Right Database

### When to Use SQL

✅ **Choose SQL when you need:**
- Complex relationships between data
- ACID transactions (banking, e-commerce)
- Structured, consistent data
- Complex queries and joins
- Mature ecosystem and tools

**Examples:**
- E-commerce platforms
- Banking systems
- ERP/CRM systems
- Inventory management

### When to Use NoSQL

✅ **Choose NoSQL when you need:**
- Flexible schema (evolving data structure)
- Horizontal scaling (millions of users)
- Fast read/write performance
- Hierarchical/nested data
- Real-time applications

**Examples:**
- Social media feeds
- Real-time analytics
- Content management systems
- IoT applications
- Gaming leaderboards

### 🧠 Pro Tip: You Can Use Both!

Modern applications often use:
- **SQL** for critical transactional data
- **NoSQL** for caching, sessions, logs
- **Combination** for optimal performance

---

## 🛡️ Part 5 · Best Practices

### 🔒 Security

```sql
-- ❌ NEVER do this (SQL Injection risk)
query = "SELECT * FROM users WHERE name = '" + userInput + "'"

-- ✅ Use parameterized queries
query = "SELECT * FROM users WHERE name = ?"
execute(query, [userInput])
```

### ⚡ Performance

```sql
-- Create indexes for frequently queried columns
CREATE INDEX idx_email ON users(email);
CREATE INDEX idx_age ON users(age);

-- Use EXPLAIN to analyze queries
EXPLAIN SELECT * FROM users WHERE email = 'alice@email.com';
```

### 📋 Data Integrity

```sql
-- Use constraints
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    email TEXT UNIQUE NOT NULL,
    age INTEGER CHECK (age >= 0 AND age <= 150)
);

-- Use transactions for multiple operations
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### 🗄️ Backup and Recovery

```bash
# SQL backup
mysqldump -u root -p database_name > backup.sql

# MongoDB backup
mongodump --db database_name --out /backup/

# Restore
mysql -u root -p database_name < backup.sql
mongorestore /backup/
```

---

## 🤖 AI Tip · Database Mastery

### ✅ Smart Prompts:

- *"Explain the difference between INNER JOIN and LEFT JOIN"*
- *"Write a SQL query to find duplicate emails"*
- *"Design a database schema for a blog platform"*
- *"What's the best way to store hierarchical data in SQL?"*
- *"Optimize this slow MongoDB query"*

### 🎯 AI Can Help With:

- Query optimization
- Schema design
- Explaining complex joins
- Converting SQL to NoSQL (and vice versa)
- Debugging database errors

---

## 🎯 Mission · Day 07

**Master data management** 💾

- [ ] 📊 Create a SQL table with at least 3 columns
- [ ] ✨ Insert 5 records into your table
- [ ] 🔍 Write a SELECT query with a WHERE clause
- [ ] ✏️ Update a record based on a condition
- [ ] 🗑️ Delete a record safely
- [ ] 🔗 Create two related tables with a foreign key

### Bonus Challenge ⭐

- [ ] Design a complete database schema for a todo app (users, tasks, categories)
- [ ] Write a query that joins 3 tables
- [ ] Compare SQL vs NoSQL for a specific use case
- [ ] Set up a local MongoDB instance and perform CRUD operations
- [ ] Implement pagination (LIMIT and OFFSET)

---

## 📚 Common SQL Patterns

### Pagination
```sql
-- Page 1 (10 results per page)
SELECT * FROM users LIMIT 10 OFFSET 0;

-- Page 2
SELECT * FROM users LIMIT 10 OFFSET 10;

-- Page 3
SELECT * FROM users LIMIT 10 OFFSET 20;
```

### Finding Duplicates
```sql
SELECT email, COUNT(*)
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

### Upsert (Insert or Update)
```sql
-- SQLite
INSERT OR REPLACE INTO users (id, name, email)
VALUES (1, 'Alice', 'alice@email.com');

-- PostgreSQL
INSERT INTO users (id, name, email)
VALUES (1, 'Alice', 'alice@email.com')
ON CONFLICT (id) DO UPDATE SET
  name = EXCLUDED.name,
  email = EXCLUDED.email;
```

---

<div align="center">

## 🏆 Achievement Unlocked

### *"The Data Architect"*

**You now understand:**
- SQL and relational databases
- NoSQL and document databases
- CRUD operations in both paradigms
- When to use each type
- Security and best practices

You're no longer just storing data.  
**You're designing information systems.**

---

### 🎓 Pro Tip

> "Database design is permanent.  
> Spend time planning before coding.  
> A good schema today saves weeks of refactoring tomorrow."

---

➡️ [Continue to Chapter 08 · APIs & Integration](../08-APIs/README.md)

</div>
