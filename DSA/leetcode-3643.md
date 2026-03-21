# 📌 Flip Square Submatrix Vertically

## 🧠 Problem Overview
Given a 2D grid and three integers `x`, `y`, and `k`, reverse a `k × k` submatrix starting from position `(x, y)`.

- The operation performs a **vertical flip** of the selected submatrix.
- The modified grid is returned as the result.

---

## 🚀 Approach

### 🔹 Identify Submatrix Boundaries
- Top-left corner → `(x, y)`
- Bottom-right corner → `(x + k - 1, y + k - 1)`

---

### 🔹 Perform Vertical Reversal
- Swap rows from top to bottom within the submatrix:
  - First row ↔ Last row
  - Second row ↔ Second-last row
  - Continue until the middle is reached

- Only columns within the submatrix are swapped

---

### 🔹 Key Idea
This is similar to reversing rows of a matrix **within a restricted region**.

---
## 💻 Implementation

```cpp
class Solution {
public:
    vector<vector<int>> reverseSubmatrix(vector<vector<int>>& grid, int x, int y, int k) {

        int startRow = x;
        int endRow = x + k - 1;
        int startCol = y;
        int endCol = y + k - 1;

        while (startRow <= endRow) {
            for (int j = startCol; j <= endCol; j++) {
                swap(grid[startRow][j], grid[endRow][j]);
            }
            startRow++;
            endRow--;
        }

        return grid;
    }
};
```

---
## 📊 Example

### Input
```
grid = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
], x = 0, y = 0, k = 2
```

### Submatrix (before)
```
[1, 2]
[4, 5]
```

### After Vertical Flip
```
[4, 5]
[1, 2]
```

### Output
```
[
  [4, 5, 3],
  [1, 2, 6],
  [7, 8, 9]
]
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(k²)`  
  (Processing all elements of the submatrix)

- **Space Complexity:** `O(1)`  
  (In-place modification)

---
