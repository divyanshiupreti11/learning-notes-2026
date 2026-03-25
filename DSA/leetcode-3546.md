# 📌 Equal Sum Grid Partition I
## 🧠 Problem Overview
Given a 2D grid of integers, determine whether it is possible to partition the grid into two parts such that:

- The **sum of elements in both parts is equal**
- The partition can be made using:
  - A **horizontal cut** (between rows), or
  - A **vertical cut** (between columns)

Return `true` if such a partition exists, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Step 1: Compute Total Sum
- Calculate the total sum of all elements in the grid
- If the total sum is **odd**, equal partition is impossible

```
if (totalSum % 2 != 0) → return false
```

---

### 🔹 Step 2: Target Sum
- The goal is to find a partition such that each part has:
```
target = totalSum / 2
```

---

### 🔹 Step 3: Check Horizontal Partition
- Traverse rows from top to bottom
- Keep adding row sums until:
  - Either sum equals target → valid partition
  - Or exceeds target → stop

---

### 🔹 Step 4: Check Vertical Partition
- Traverse columns from left to right
- Accumulate column sums
- If at any point sum equals target → valid partition

---
## 💻 Implementation

```cpp
class Solution {
public:
    static bool canPartitionGrid(vector<vector<int>>& grid) {

        long long totalSum = 0;

        // Step 1: Compute total sum
        for (auto& row : grid) {
            totalSum += accumulate(row.begin(), row.end(), 0LL);
        }

        // If sum is odd, cannot partition
        if (totalSum & 1) return false;

        long long target = totalSum / 2;

        int rows = grid.size();
        int cols = grid[0].size();

        long long rowSum = 0;

        // Step 2: Check horizontal partition
        for (int i = 0; i < rows && rowSum < target; i++) {
            rowSum += accumulate(grid[i].begin(), grid[i].end(), 0LL);
        }

        if (rowSum == target) return true;

        long long colSum = 0;

        // Step 3: Check vertical partition
        for (int j = 0; j < cols && colSum < target; j++) {
            for (int i = 0; i < rows; i++) {
                colSum += grid[i][j];
            }
        }

        return colSum == target;
    }
};
```

---
