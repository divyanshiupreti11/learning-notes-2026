# 📌 Matrix Similarity After Cyclic Shifts
## 🧠 Problem Overview
Given a 2D matrix `mat` and an integer `k`, determine whether the matrix remains **unchanged** after performing cyclic shifts on each row:

- **Even-indexed rows (0-based)** → shifted **right** by `k` positions  
- **Odd-indexed rows** → shifted **left** by `k` positions  

Return `true` if the matrix remains identical after the operation, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Normalize Shifts
- Since shifting by `n` (number of columns) results in the same row:
```
k = k % n
```

- If `k == 0`, no change occurs → return `true`

---

### 🔹 Simulate Index Mapping
Instead of actually shifting rows, we compare positions using index transformation.

For each element `mat[i][j]`:

#### ✅ Even Row (Right Shift)
```
finalIndex = (j + k) % n
```

#### ✅ Odd Row (Left Shift)
```
finalIndex = (j - k + n) % n
```

---

### 🔹 Validation
- Compare:
```
mat[i][j] == mat[i][finalIndex]
```
- If any mismatch occurs → return `false`

---

