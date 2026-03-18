# 📌 Count Submatrices With Sum ≤ K
# 🔗 Problem Link
https://leetcode.com/problems/count-submatrices-with-top-left-element-and-sum-less-than-k/?envType=daily-question&envId=2026-03-18

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
## 📊 Example

### Input
```
grid = [
  [1, 2],
  [3, 4]
], k = 7
```

### Prefix Sum Matrix
```
[
  [0, 0, 0],
  [0, 1, 3],
  [0, 4, 10]
]
```

### Valid Submatrices (Top-left based)
- (0,0) → sum = 1 ✅  
- (0,1) → sum = 3 ✅  
- (1,0) → sum = 4 ✅  
- (1,1) → sum = 10 ❌  

### Output
```
Count = 3
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`  
  (Single pass through the matrix)

- **Space Complexity:** `O(m × n)`  
  (Prefix sum matrix)

---
