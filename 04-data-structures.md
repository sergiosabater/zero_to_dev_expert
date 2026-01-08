<div align="center">

# 🧱 Chapter 04 · Data Structures

### Arrays · Trees · Big-O Notation

![Data Structures](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExY2V5c3Q1MndmY3J2NHN4c3B2YTRpY2p4Y3d4Y2ZpZ3h0dHk3eSZlcD12MV9naWZfYnlfaWQmY3Q9Zw/13HgwGsXF0aiGY/giphy.gif)

> *"Good code works. Great code scales."*

[🔙 Back to Chapter 03](./03-programming-basics.md)

</div>

---

## 🧠 Why Data Structures Matter

Programs don't just **do things**.  
They **store, organize, and retrieve data**.

A **data structure** is the way you organize information so your program can:

- 🚀 Run faster
- 📈 Scale better
- 🧠 Be easier to reason about

> 💡 *Choosing the right data structure often matters more than the language itself.*

---

## 📦 Part 1 · Arrays

### *Ordered Collections*

An **array** is a list of elements stored in order.

Think of it like:
> 🧺 A row of numbered boxes

### 🐍 Python Example

```python
numbers = [10, 20, 30, 40]
names = ["Alice", "Bob", "Charlie"]
```

### 🟨 JavaScript Example

```javascript
let numbers = [10, 20, 30, 40];
let names = ["Alice", "Bob", "Charlie"];
```

### 🔎 Accessing Elements

**Python:**
```python
numbers[0]   # 10
numbers[2]   # 30
```

**JavaScript:**
```javascript
numbers[0];  // 10
numbers[2];  // 30
```

### 🧠 Key Ideas

✅ Arrays are **ordered**  
✅ Each element has an **index**  
✅ Access by index is **fast**

⚠️ **But:**
- Inserting or deleting in the middle can be expensive

---

## 🌳 Part 2 · Trees

### *Hierarchical Thinking*

A **tree** organizes data in a parent → child structure.

**Examples in real life:**
- 📁 File systems
- 🌐 HTML / DOM
- 🧠 Decision processes

```
        Root
       /    \
   Child A  Child B
     /
 Grandchild
```

### 🧠 Tree Vocabulary

| Term | Meaning |
|------|---------|
| 🌱 **Root** | Top element |
| 🌿 **Node** | Each element |
| 🍃 **Leaf** | Node with no children |
| 🌲 **Depth/Height** | Distance from root |

### 💡 Why Trees Matter

Trees allow:
- ⚡ Fast searching
- 🎯 Natural hierarchy modeling
- 🧠 Efficient decision making

> Most advanced systems rely heavily on trees under the hood.

---

## ⏱️ Part 3 · Big-O Notation

### *How Fast (or Slow) Is Your Code?*

**Big-O** describes how your algorithm's performance grows as the input size increases.

It's not about exact time, but about **scaling behavior**.

### 📊 Common Big-O Cases

| Big-O | Name | Example |
|-------|------|---------|
| **O(1)** | Constant | Access array element |
| **O(n)** | Linear | Loop through array |
| **O(n²)** | Quadratic | Nested loops |
| **O(log n)** | Logarithmic | Binary search |
| **O(n log n)** | Efficient sort | Merge sort |

### 🧪 Example: Linear Time

```python
for number in numbers:
    print(number)
```

➡️ If the array doubles, the work doubles → **O(n)**

### 🧪 Example: Quadratic Time

```python
for i in numbers:
    for j in numbers:
        print(i, j)
```

➡️ If the array doubles, the work quadruples → **O(n²)**

⚠️ **This does not scale well.**

### 🧠 Mental Model

Ask yourself:

- 📈 What happens if my data grows 10×?
- 🔄 Am I looping inside another loop?
- 🧱 Is there a better structure for this problem?

> Big-O is about thinking ahead, not micro-optimizing.

---

## 🤖 AI Tip · Ask Smarter Questions

### ✅ Great AI prompts:

- *"What is the Big-O of this code?"*
- *"Can this be optimized with a different data structure?"*
- *"Explain this algorithm like I'm 10"*

### ❌ Bad prompt:

- *"Optimize this"* (without context)

---

## 🎯 Mission · Day 04

**Time to level up** ⚔️

- [ ] 📦 Create an array of 5 numbers and print each one
- [ ] 🌳 Draw a simple tree on paper (root + children)
- [ ] ⏱️ Identify the Big-O of a simple loop
- [ ] 🤖 Ask AI to explain why O(n²) is dangerous

### Bonus Challenge ⭐

- [ ] Rewrite a nested loop to reduce its complexity
- [ ] Explain the difference between O(n) and O(log n) in your own words

---

<div align="center">

## 🏆 Achievement Unlocked

### *"The Architect"*

**You now understand:**
- Arrays
- Trees
- Algorithmic complexity

You're no longer just writing code —  
**you're designing systems.**

---

➡️ [Continue to Chapter 05 · Algorithms & Problem Solving](../05-Algorithms/README.md)

</div>
