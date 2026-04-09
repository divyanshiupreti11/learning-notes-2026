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
## 🔹 Step 1: Handle Large K

For large step size:
```
for (i = L; i <= R; i += K)
    nums[i] *= V
```

👉 Number of updates is small → efficient

---

## 🔹 Step 2: Group Small K Queries

- Store queries based on same `K`
- Process them together using a **difference array**

---

## 🔹 Step 3: Difference Array Trick

Instead of updating each index:

- Apply multiplication at start:
```
diff[L] *= V
```

- Apply inverse at end:
```
diff[next] *= inverse(V)
```

---

## 🔹 Step 4: Prefix Propagation

For same step `K`:
```
diff[i] *= diff[i-K]
```

👉 This spreads updates efficiently

---

## 🔹 Step 5: Apply Updates

```
nums[i] = nums[i] * diff[i]
```

---

## 🔹 Step 6: Compute XOR

```
result = nums[0] ^ nums[1] ^ ... ^ nums[n-1]
```

---

