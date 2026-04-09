# 📌 XOR After Range Multiplication Queries II
## 🧠 Problem Description

You are given:

- An array `nums`
- A list of queries `queries[][]`

Each query is of the form:
```
[L, R, K, V]
```

### 📌 Query Meaning
For each query:
- Start at index `L`
- Move with step size `K`
- For all indices `i ≤ R`:
```
nums[i] = (nums[i] × V) % (1e9 + 7)
```

---

## 🎯 Objective

After processing all queries, return the **bitwise XOR** of all elements in the final array.

---

## 🚀 Approach

### 🔹 Key Idea: √ Decomposition Optimization

👉 Direct simulation is too slow for small `K`  
👉 We split queries into:

- **Large K (K ≥ √n)** → process directly  
- **Small K (K < √n)** → optimize using prefix technique  

---
