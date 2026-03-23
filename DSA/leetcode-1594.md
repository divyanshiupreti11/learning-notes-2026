#  📌 Maximum Non Negative Product in a Matrix

## 🧠 Problem Overview
Given a 2D grid of integers (which may include positive, negative, and zero values), find the **maximum non-negative product** of a path from the **top-left corner `(0,0)` to the bottom-right corner `(m-1,n-1)`**.

- You can only move **right** or **down**
- If the maximum product is negative, return `-1`
- Otherwise, return the result modulo `1e9 + 7`

---

## 🚀 Approach

### 🔹 Key Challenge
- The grid contains **negative values**, which can flip signs
- A minimum product can become maximum after multiplying by a negative number

👉 Therefore, we must track:
- **Maximum product**
- **Minimum product**

at each cell

---

### 🔹 Dynamic Programming with Memoization

We use a recursive function with memoization:

```
solve(i, j) → returns {maxProduct, minProduct} from (i, j) to destination
```

---

### 🔹 Transition Logic

From each cell `(i, j)`:
- Move **down** → `(i+1, j)`
- Move **right** → `(i, j+1)`

For both directions:
- Multiply current value with:
  - next cell's max product
  - next cell's min product

Update:
```
maxVal = max(all possible products)
minVal = min(all possible products)
```

---

### 🔹 Base Case
```
If (i, j) == (m-1, n-1):
    return {grid[i][j], grid[i][j]}
```

---
