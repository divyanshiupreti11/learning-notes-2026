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
## 💻 Implementation

```cpp
class Solution {
public:
    bool areSimilar(vector<vector<int>>& mat, int k) {
        int m = mat.size();
        int n = mat[0].size();

        k = k % n;

        if (k == 0) return true;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                int finalIdx;

                if (i % 2 == 0) {
                    // Right shift
                    finalIdx = (j + k) % n;
                } else {
                    // Left shift
                    finalIdx = (j - k + n) % n;
                }

                if (mat[i][j] != mat[i][finalIdx]) {
                    return false;
                }
            }
        }

        return true;
    }
};
```

---
## 📊 Example

### Input
```
mat = [
  [1, 2, 3],
  [4, 5, 6]
], k = 1
```

### After Shifts
- Row 0 (even) → right shift → `[3, 1, 2]`
- Row 1 (odd) → left shift → `[5, 6, 4]`

### Comparison
- New matrix ≠ original matrix ❌

### Output
```
false
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`  
- **Space Complexity:** `O(1)`  
  (No extra space used)

---
