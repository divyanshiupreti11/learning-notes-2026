# 📌 Equal Sum Grid Partition II
## 🧠 Problem Overview
Given a 2D grid of integers, determine whether it is possible to partition the grid into two parts such that:

- The two parts have **equal sum**, OR
- The difference between the two parts can be balanced by **removing a single element** from one side

### Allowed Operations
- Partition using:
  - **Horizontal cuts**
  - **Vertical cuts**

---

## 🚀 Approach

### 🔹 Step 1: Compute Total Sum
- Calculate the sum of all elements in the grid:
```
totalSum = sum of all elements
```

---

### 🔹 Step 2: Horizontal Partition Check

We simulate horizontal cuts row by row:

- Maintain:
  - `top` → sum of upper part
  - `bottom = totalSum - top`
  - `diff = top - bottom`

---

### 🔹 Step 3: Handle Cases

At each cut:

#### ✅ Case 1: Perfect Partition
```
if (diff == 0) → valid partition
```

#### ✅ Case 2: Fix by Removing One Element
Check if removing one element can balance:

- Edge cases:
  - Top-left element → `grid[0][0]`
  - Top-right element → `grid[0][n-1]`
  - Current row boundary → `grid[i][0]`

- General case:
  - Use a set to track all elements in the top portion
  - If `diff` exists in the set → valid

---

### 🔹 Step 4: Cover All Directions

To handle all possible partitions:

1. Original grid → horizontal cuts  
2. Reverse grid → simulate bottom cuts  
3. Transpose grid → convert vertical cuts into horizontal  
4. Reverse transposed grid → cover remaining cases  

---
