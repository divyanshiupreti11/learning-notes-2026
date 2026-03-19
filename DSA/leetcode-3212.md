# 📌 Number of Submatrices With Equal X and Y
# 🔗 Problem link 
https://leetcode.com/problems/count-submatrices-with-equal-frequency-of-x-and-y/description/?envType=daily-question&envId=2026-03-19

## 🧠 Problem Overview
Given a 2D grid consisting of characters `'X'` and `'Y'`, determine the number of submatrices (from the top-left corner `(0,0)` to `(i,j)`) such that:

- The count of `'X'` is equal to the count of `'Y'`
- The count of `'X'` is greater than `0`

---

## 🚀 Approach

### 🔹 2D Prefix Count Technique
We maintain two prefix matrices:

- `px[i][j]` → Number of `'X'` characters from `(0,0)` to `(i,j)`
- `py[i][j]` → Number of `'Y'` characters from `(0,0)` to `(i,j)`

---

### 🔹 Transition Formula

For each cell `(i, j)`:

```
px[i][j] = (grid[i][j] == 'X')
py[i][j] = (grid[i][j] == 'Y')

px[i][j] += px[i-1][j] + px[i][j-1] - px[i-1][j-1]
py[i][j] += py[i-1][j] + py[i][j-1] - py[i-1][j-1]
```

This ensures we correctly accumulate counts using inclusion-exclusion.

---

### 🔹 Counting Valid Submatrices

At each cell `(i, j)`:
- If `px[i][j] == py[i][j]`  
- And `px[i][j] > 0`  

Then increment the answer.

---

## 💻 Implementation

```cpp
class Solution {
public:
    int numberOfSubmatrices(vector<vector<char>>& grid) {
        int m = grid.size(), n = grid[0].size();
        int ans = 0;

        vector<vector<int>> px(m, vector<int>(n, 0));
        vector<vector<int>> py(m, vector<int>(n, 0));

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                px[i][j] = (grid[i][j] == 'X');
                py[i][j] = (grid[i][j] == 'Y');

                if (i > 0) {
                    px[i][j] += px[i - 1][j];
                    py[i][j] += py[i - 1][j];
                }
                if (j > 0) {
                    px[i][j] += px[i][j - 1];
                    py[i][j] += py[i][j - 1];
                }
                if (i > 0 && j > 0) {
                    px[i][j] -= px[i - 1][j - 1];
                    py[i][j] -= py[i - 1][j - 1];
                }

                if (px[i][j] == py[i][j] && px[i][j] > 0) {
                    ans++;
                }
            }
        }

        return ans;
    }
};
```

---

## 📊 Example

### Input
```
grid = [
  ['X', 'Y'],
  ['Y', 'X']
]
```

### Prefix Count Matrices

#### px (count of X)
```
[
  [1, 1],
  [1, 2]
]
```

#### py (count of Y)
```
[
  [0, 1],
  [1, 2]
]
```

### Valid Submatrices
- (0,1) → X = 1, Y = 1 ✅  
- (1,0) → X = 1, Y = 1 ✅  
- (1,1) → X = 2, Y = 2 ✅  

### Output
```
Count = 3
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`  
- **Space Complexity:** `O(m × n)`
