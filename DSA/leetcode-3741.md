
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

---

## 🚀 Key Insight

Since `i < j < k`, the formula simplifies to:

```
distance = 2 × (k - i)
```

👉 Only the **first and third index matter**

---

## 🚀 Approach (Optimized)

### 🔹 Step 1: Track Indices Using HashMap

- Use a map:
```
value → list of indices
```

---

### 🔹 Step 2: Process Array in One Pass

For each index `k`:

- Add index `k` to the list of `nums[k]`
- If the list size becomes ≥ 3:
  - Take last 3 indices:
```
i = vec[size - 3]
k = current index
```

---

### 🔹 Step 3: Compute Distance

```
distance = 2 × (k - i)
```

- Update minimum result

---

### 🔹 Step 4: Return Answer

- If no valid triplet → return `-1`

---
