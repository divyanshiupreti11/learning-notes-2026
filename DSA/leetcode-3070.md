# 📌 Count Submatrices With Sum ≤ K

## 🧠 Problem Overview
Given a 2D grid of integers and an integer `k`, return the number of submatrices whose sum is **less than or equal to `k`**.

A submatrix is defined as a contiguous rectangular region within the grid.

---

## 🚀 Approach

### 🔹 Prefix Sum Technique (2D)
To efficiently compute submatrix sums, we use a **2D prefix sum matrix**.

- Let `px[i][j]` represent the sum of elements from `(0,0)` to `(i-1, j-1)`.

The prefix sum is computed as:
```
px[i+1][j+1] = grid[i][j] 
             + px[i][j+1] 
             + px[i+1][j] 
             - px[i][j]
```

---

### 🔹 Counting Valid Submatrices
- While building the prefix sum matrix, we check:
  ```
  if px[i+1][j+1] ≤ k → increment count
  ```
- Each valid prefix represents a submatrix from `(0,0)` to `(i,j)`.

---

