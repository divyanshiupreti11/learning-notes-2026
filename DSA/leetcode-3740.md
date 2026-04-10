# 📌 Minimum Distance Between Three Equal Elements I
## 🧠 Problem Description

You are given an integer array `nums`.

### 🎯 Objective
Find the **minimum distance** between any triplet `(i, j, k)` such that:

- `i < j < k`
- `nums[i] == nums[j] == nums[k]`

### 📌 Distance Formula
```
distance = |i - j| + |j - k| + |k - i|
```

👉 If no such triplet exists, return `-1`.

---

## 🚀 Approach (Brute Force)

### 🔹 Step 1: Try All Triplets
- Use three nested loops:
  - `i` from `0 → n-1`
  - `j` from `i+1 → n-1`
  - `k` from `j+1 → n-1`

---

### 🔹 Step 2: Check Condition
```
if nums[i] == nums[j] == nums[k]
```

---

### 🔹 Step 3: Compute Distance
```
dist = |i - j| + |j - k| + |k - i|
```

- Keep track of the **minimum distance**

---

### 🔹 Step 4: Return Result
- If no valid triplet found → return `-1`

---
