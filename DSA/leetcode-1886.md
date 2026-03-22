# Determine Whether Matrix Can Be Obtained By Rotation


## 🧠 Problem Overview
Given two `n × n` binary matrices `mat` and `target`, determine whether `mat` can be transformed into `target` by rotating it in multiples of **90 degrees clockwise**.

You may perform at most **4 rotations** (0°, 90°, 180°, 270°).

---

## 🚀 Approach

### 🔹 Matrix Rotation (90° Clockwise)
To rotate a matrix by 90° clockwise:

1. **Transpose the matrix**
   - Swap `mat[i][j]` with `mat[j][i]`

2. **Reverse each row**
   - This completes the rotation

---

### 🔹 Check Equality After Each Rotation
- Compare `mat` with `target`
- If they match → return `true`
- Otherwise, rotate and repeat

- Perform this process **up to 4 times**

---

## 💻 Implementation

```cpp
class Solution {
public:

    // Function to rotate matrix by 90 degrees clockwise
    void rotate(vector<vector<int>>& mat, int n) {
        // Step 1: Transpose
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                swap(mat[i][j], mat[j][i]);
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; i++) {
            reverse(mat[i].begin(), mat[i].end());
        }
    }

    bool findRotation(vector<vector<int>>& mat, vector<vector<int>>& target) {
        int n = mat.size();

        for (int count = 1; count <= 4; count++) {
            bool isEqual = true;

            // Compare matrices
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (mat[i][j] != target[i][j]) {
                        isEqual = false;
                        break;
                    }
                }
                if (!isEqual) break;
            }

            if (isEqual) return true;

            // Rotate matrix for next comparison
            rotate(mat, n);
        }

        return false;
    }
};
```

---

## 📊 Example

### Input
```
mat = [
  [0, 1],
  [1, 0]
]

target = [
  [1, 0],
  [0, 1]
]
```

### Rotation Steps

#### Original (0°)
```
[0, 1]
[1, 0]
```

#### After 90° Rotation
```
[1, 0]
[0, 1]
```

✅ Matches target → return `true`

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n²)` per rotation  
  → Total: `O(4 × n²)` ≈ `O(n²)`

- **Space Complexity:** `O(1)`  
  (In-place rotation)

---
