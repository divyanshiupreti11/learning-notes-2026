# 📌 Equal Sum Grid Partition II
## 🔗 Problem Link
https://leetcode.com/problems/equal-sum-grid-partition-ii/description/?envType=daily-question&envId=2026-03-26
## 🧠 Problem Overview
Given a 2D grid of integers, determine whether it is possible to partition the grid into two parts such that:

- The two parts have **equal sum**, OR
- The difference between the two parts can be balanced by **removing a single element** from one side

### Allowed Operations
- Partition using:
  - **Horizontal cuts**
  - **Vertical cuts**

---

## 🚀 Approach

### 🔹 Step 1: Compute Total Sum
- Calculate the sum of all elements in the grid:
```
totalSum = sum of all elements
```

---

### 🔹 Step 2: Horizontal Partition Check

We simulate horizontal cuts row by row:

- Maintain:
  - `top` → sum of upper part
  - `bottom = totalSum - top`
  - `diff = top - bottom`

---

### 🔹 Step 3: Handle Cases

At each cut:

#### ✅ Case 1: Perfect Partition
```
if (diff == 0) → valid partition
```

#### ✅ Case 2: Fix by Removing One Element
Check if removing one element can balance:

- Edge cases:
  - Top-left element → `grid[0][0]`
  - Top-right element → `grid[0][n-1]`
  - Current row boundary → `grid[i][0]`

- General case:
  - Use a set to track all elements in the top portion
  - If `diff` exists in the set → valid

---

### 🔹 Step 4: Cover All Directions

To handle all possible partitions:

1. Original grid → horizontal cuts  
2. Reverse grid → simulate bottom cuts  
3. Transpose grid → convert vertical cuts into horizontal  
4. Reverse transposed grid → cover remaining cases  

---
## 💻 Implementation

```cpp
class Solution {
public:
    typedef long long ll;

    ll totalSum = 0;

    bool checkHorCut(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        unordered_set<ll> st;
        ll top = 0;

        for (int i = 0; i < m - 1; i++) {
            for (int j = 0; j < n; j++) {
                st.insert(grid[i][j]);
                top += grid[i][j];
            }

            ll bottom = totalSum - top;
            ll diff = top - bottom;

            // Case 1: Equal partition
            if (diff == 0) return true;

            // Case 2: Edge removals
            if (diff == (ll)grid[0][0]) return true;
            if (diff == (ll)grid[0][n - 1]) return true;
            if (diff == (ll)grid[i][0]) return true;

            // Case 3: General removal
            if (i > 0 && n > 1 && st.count(diff)) return true;
        }

        return false;
    }

    bool canPartitionGrid(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        // Compute total sum
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                totalSum += grid[i][j];
            }
        }

        // Check all configurations
        if (checkHorCut(grid)) return true;

        reverse(grid.begin(), grid.end());
        if (checkHorCut(grid)) return true;
        reverse(grid.begin(), grid.end());

        // Transpose grid
        vector<vector<int>> transposeGrid(n, vector<int>(m));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                transposeGrid[j][i] = grid[i][j];
            }
        }

        if (checkHorCut(transposeGrid)) return true;

        reverse(transposeGrid.begin(), transposeGrid.end());
        if (checkHorCut(transposeGrid)) return true;

        return false;
    }
};
```

---
## 📊 Example

### Input
```
grid = [
  [2, 1, 3],
  [1, 2, 1]
]
```

### Explanation
- Total sum = 10
- Try different cuts
- If direct partition fails, check if removing one element balances the difference

### Output
```
true / false (depending on configuration)
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`  
  (Each configuration is processed efficiently)

- **Space Complexity:** `O(m × n)`  
  (Set + transpose grid)

---
