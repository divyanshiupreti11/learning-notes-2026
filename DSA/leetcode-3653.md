# 📌 XOR After Range Multiplication Queries I
## 🧠 Problem Description

You are given:

- An array `nums`
- A list of queries `queries[][]`

Each query contains:
```
[l, r, k, v]
```

### 📌 Query Meaning
For each query:
- Start from index `l`
- Move with step size `k`
- Continue while index ≤ `r`
- For every such index:
```
nums[i] = (nums[i] × v) % (1e9 + 7)
```

---

## 🎯 Objective

After processing all queries, return the **bitwise XOR** of all elements in the final array.

---

## 🚀 Approach

### 🔹 Step 1: Process Each Query

For every query:
- Extract values:
  - `l` → starting index
  - `r` → ending index
  - `k` → step size
  - `v` → multiplier

- Iterate:
```
for (i = l; i <= r; i += k)
    nums[i] = (nums[i] * v) % MOD
```

---

### 🔹 Step 2: Compute XOR

After applying all queries:
```
result = nums[0] ^ nums[1] ^ ... ^ nums[n-1]
```

---
