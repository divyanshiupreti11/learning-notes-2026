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
## 💻 Implementation

```cpp
class Solution {
public:
    int countSubmatrices(vector<vector<int>>& grid, int k) {
        int count = 0;
        int m = grid.size(), n = grid[0].size();

        vector<vector<int>> prefix(m + 1, vector<int>(n + 1, 0));

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                prefix[i + 1][j + 1] = grid[i][j]
                                    + prefix[i][j + 1]
                                    + prefix[i + 1][j]
                                    - prefix[i][j];

                if (prefix[i + 1][j + 1] <= k) {
                    count++;
                }
            }
        }

        return count;
    }
};
```

---

