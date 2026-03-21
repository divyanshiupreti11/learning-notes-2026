# 📌 Flip Square Submatrix Vertically

## 🧠 Problem Overview
Given a 2D grid and three integers `x`, `y`, and `k`, reverse a `k × k` submatrix starting from position `(x, y)`.

- The operation performs a **vertical flip** of the selected submatrix.
- The modified grid is returned as the result.

---

## 🚀 Approach

### 🔹 Identify Submatrix Boundaries
- Top-left corner → `(x, y)`
- Bottom-right corner → `(x + k - 1, y + k - 1)`

---

### 🔹 Perform Vertical Reversal
- Swap rows from top to bottom within the submatrix:
  - First row ↔ Last row
  - Second row ↔ Second-last row
  - Continue until the middle is reached

- Only columns within the submatrix are swapped

---

### 🔹 Key Idea
This is similar to reversing rows of a matrix **within a restricted region**.

---
