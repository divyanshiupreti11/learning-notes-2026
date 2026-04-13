# 📌 Minimum Distance to the Target Element

## 🧠 Problem Description

You are given:

- An integer array `nums`
- An integer `target`
- An integer `start` representing a starting index

### 🎯 Objective
Find the **minimum distance** between the `start` index and any index `i` such that:

```
nums[i] == target
```

### 📌 Distance Definition
```
distance = |i - start|
```

---

## 🚀 Approach

### 🔹 Step 1: Traverse the Array
- Iterate through all indices of the array

---

### 🔹 Step 2: Check for Target
- If:
```
nums[i] == target
```
- Compute:
```
distance = abs(i - start)
```

---

### 🔹 Step 3: Track Minimum Distance
- Maintain a variable `minDistance`
- Update it whenever a smaller distance is found

---

### 🔹 Step 4: Return Result
- Return the minimum distance found

---
