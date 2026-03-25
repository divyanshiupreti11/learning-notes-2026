# 📌 Equal Sum Grid Partition I
## 🧠 Problem Overview
Given a 2D grid of integers, determine whether it is possible to partition the grid into two parts such that:

- The **sum of elements in both parts is equal**
- The partition can be made using:
  - A **horizontal cut** (between rows), or
  - A **vertical cut** (between columns)

Return `true` if such a partition exists, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Step 1: Compute Total Sum
- Calculate the total sum of all elements in the grid
- If the total sum is **odd**, equal partition is impossible

```
if (totalSum % 2 != 0) → return false
```

---

### 🔹 Step 2: Target Sum
- The goal is to find a partition such that each part has:
```
target = totalSum / 2
```

---

### 🔹 Step 3: Check Horizontal Partition
- Traverse rows from top to bottom
- Keep adding row sums until:
  - Either sum equals target → valid partition
  - Or exceeds target → stop

---

### 🔹 Step 4: Check Vertical Partition
- Traverse columns from left to right
- Accumulate column sums
- If at any point sum equals target → valid partition

---
