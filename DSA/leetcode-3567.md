# 📌 Minimum Absolute Difference in K×K Submatrices
# 🔗 Problem Link
https://leetcode.com/problems/minimum-absolute-difference-in-sliding-submatrix/description/?envType=daily-question&envId=2026-03-20

## 🧠 Problem Overview
Given a 2D integer grid and an integer `k`, compute a matrix `result` such that:

- Each `result[i][j]` represents the **minimum absolute difference** between any two distinct elements  
  in the `k × k` submatrix starting at `(i, j)`.

---

## 🚀 Approach

### 🔹 Sliding Window over Submatrices
- Iterate over all possible `k × k` submatrices
- For each top-left corner `(i, j)`, process the submatrix from:
  ```
  (i, j) → (i + k - 1, j + k - 1)
  ```

---

### 🔹 Use Ordered Set
- Insert all elements of the current submatrix into a **sorted set**
- This ensures elements are stored in ascending order

---

### 🔹 Compute Minimum Absolute Difference
- If all elements are identical → result is `0`
- Otherwise:
  - Traverse the sorted set
  - Compute differences between **adjacent elements**
  - Track the minimum difference
    ---

## 💻 Implementation

```cpp
class Solution {
public:
    vector<vector<int>> minAbsDiff(vector<vector<int>>& grid, int k) {
        int m = grid.size();
        int n = grid[0].size();

        vector<vector<int>> result(m - k + 1, vector<int>(n - k + 1));

        for (int i = 0; i <= m - k; i++) {
            for (int j = 0; j <= n - k; j++) {

                set<int> values;

                // Collect elements of k x k submatrix
                for (int r = i; r < i + k; r++) {
                    for (int c = j; c < j + k; c++) {
                        values.insert(grid[r][c]);
                    }
                }

                // If all elements are same
                if (values.size() == 1) {
                    result[i][j] = 0;
                    continue;
                }

                int minDiff = INT_MAX;

                auto prev = values.begin();
                auto curr = next(prev);

                while (curr != values.end()) {
                    minDiff = min(minDiff, *curr - *prev);
                    prev = curr;
                    curr++;
                }

                result[i][j] = minDiff;
            }
        }

        return result;
    }
};
```

---

## 📊 Example

### Input
```
grid = [
  [1, 3, 6],
  [7, 9, 2],
  [4, 8, 5]
], k = 2
```

### Submatrices & Results

Submatrix (0,0):
```
[1, 3]
[7, 9]
→ values = {1,3,7,9}
→ min diff = 2
```

Submatrix (0,1):
```
[3, 6]
[9, 2]
→ values = {2,3,6,9}
→ min diff = 1
```

Submatrix (1,0):
```
[7, 9]
[4, 8]
→ values = {4,7,8,9}
→ min diff = 1
```

Submatrix (1,1):
```
[9, 2]
[8, 5]
→ values = {2,5,8,9}
→ min diff = 1
```

### Output
```
[
  [2, 1],
  [1, 1]
]
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:**  
  `O((m - k + 1) × (n - k + 1) × k² log(k²))`  
  (Each submatrix uses a set for sorting)

- **Space Complexity:**  
  `O(k²)` per submatrix

---
