# 📌 Minimum Absolute Difference in K×K Submatrices

## 🧠 Problem Overview
Given a 2D integer grid and an integer `k`, compute a matrix `result` such that:

- Each `result[i][j]` represents the **minimum absolute difference** between any two distinct elements  
  in the `k × k` submatrix starting at `(i, j)`.

---

## 🚀 Approach

### 🔹 Sliding Window over Submatrices
- Iterate over all possible `k × k` submatrices
- For each top-left corner `(i, j)`, process the submatrix from:
  ```
  (i, j) → (i + k - 1, j + k - 1)
  ```

---

### 🔹 Use Ordered Set
- Insert all elements of the current submatrix into a **sorted set**
- This ensures elements are stored in ascending order

---

### 🔹 Compute Minimum Absolute Difference
- If all elements are identical → result is `0`
- Otherwise:
  - Traverse the sorted set
  - Compute differences between **adjacent elements**
  - Track the minimum difference
