# 📌 Largest Submatrix With Rearrangements

## 🧠 Problem Overview
Given a binary matrix consisting of `0`s and `1`s, you are allowed to rearrange the columns of each row independently.  

The objective is to determine the **maximum area of a submatrix** that contains only `1`s after optimal column rearrangements.

---

## 🚀 Approach

### 1. Build Heights (Histogram Concept)
Convert the matrix into a height matrix where each cell represents the number of consecutive `1`s above it (including itself).

- If `matrix[i][j] == 1`, then:
  ```
  matrix[i][j] += matrix[i - 1][j]
  ```

This step transforms each row into a histogram.

---

### 2. Sort Each Row (Descending Order)
Since column rearrangement is allowed, sort each row in **non-increasing (descending) order**.

- This helps in maximizing the width for larger heights.

---

### 3. Compute Maximum Area
For each row:
- Treat the sorted row as histogram heights
- Compute area using:
  ```
  area = height × width = matrix[i][j] × (j + 1)
  ```

Track the maximum area across all rows.

---
## 💻 Implementation

```cpp
class Solution {
public:
    int largestSubmatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        int maxArea = 0;

        // Step 1: Build height matrix
        for (int i = 1; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == 1) {
                    matrix[i][j] += matrix[i - 1][j];
                }
            }
        }

        // Step 2 & 3: Sort rows and compute max area
        for (int i = 0; i < m; i++) {
            sort(matrix[i].rbegin(), matrix[i].rend());

            for (int j = 0; j < n; j++) {
                int height = matrix[i][j];
                int width = j + 1;
                maxArea = max(maxArea, height * width);
            }
        }

        return maxArea;
    }
};
```
---
## 📊 Example

### Input
```
matrix = [
  [0, 0, 1],
  [1, 1, 1],
  [1, 0, 1]
]
```

### Height Matrix
```
[
  [0, 0, 1],
  [1, 1, 2],
  [2, 0, 3]
]
```

### After Sorting Rows
```
[
  [1, 0, 0],
  [2, 1, 1],
  [3, 2, 0]
]
```

### Output
```
Maximum Area = 4
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n log n)`  
  (Sorting each row)

- **Space Complexity:** `O(1)`  
  (In-place transformation)

---
---

