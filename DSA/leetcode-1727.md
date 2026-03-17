# 📌 Largest Submatrix With Rearrangements

## 🧠 Problem Overview
Given a binary matrix consisting of `0`s and `1`s, you are allowed to rearrange the columns of each row independently.  

The objective is to determine the **maximum area of a submatrix** that contains only `1`s after optimal column rearrangements.

---

## 🚀 Approach

### 1. Build Heights (Histogram Concept)
Convert the matrix into a height matrix where each cell represents the number of consecutive `1`s above it (including itself).

- If `matrix[i][j] == 1`, then:
  ```
  matrix[i][j] += matrix[i - 1][j]
  ```

This step transforms each row into a histogram.

---

### 2. Sort Each Row (Descending Order)
Since column rearrangement is allowed, sort each row in **non-increasing (descending) order**.

- This helps in maximizing the width for larger heights.

---

### 3. Compute Maximum Area
For each row:
- Treat the sorted row as histogram heights
- Compute area using:
  ```
  area = height × width = matrix[i][j] × (j + 1)
  ```

Track the maximum area across all rows.

---
