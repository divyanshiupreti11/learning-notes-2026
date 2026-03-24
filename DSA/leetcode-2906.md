# 📌  Construct Product Matrix
## 🧠 Problem Overview
Given a 2D grid of integers, construct a matrix `p` such that:

- Each `p[i][j]` contains the **product of all elements in the grid except `grid[i][j]`**
- All operations are performed modulo `12345`

---

## 🚀 Approach

### 🔹 Key Idea
Instead of recomputing the product for each cell (which would be expensive), we use:

- **Prefix Product**
- **Suffix Product**

👉 This allows us to compute the result in **O(n × m)** time

---

### 🔹 Step 1: Compute Suffix Products
Traverse the grid from **bottom-right → top-left**

- Maintain a running product (`suffix`)
- Store the suffix product in `p[i][j]`
- Update suffix:
  ```
  suffix = (suffix * grid[i][j]) % MOD
  ```

---

### 🔹 Step 2: Compute Prefix Products
Traverse the grid from **top-left → bottom-right**

- Maintain a running product (`prefix`)
- Multiply existing value:
  ```
  p[i][j] = (prefix * p[i][j]) % MOD
  ```
- Update prefix:
  ```
  prefix = (prefix * grid[i][j]) % MOD
  ```

---

### 🔹 Final Result
Each cell now contains:
```
Product of all elements except itself (mod 12345)
```

---
