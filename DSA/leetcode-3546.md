# 📌 Equal Sum Grid Partition I
## 🔗 Problem Link
https://leetcode.com/problems/equal-sum-grid-partition-i/description/?envType=daily-question&envId=2026-03-25
## 🧠 Problem Overview
Given a 2D grid of integers, determine whether it is possible to partition the grid into two parts such that:

- Both parts have **equal sum**
- The partition is done using:
  - A **horizontal cut** (between rows), or
  - A **vertical cut** (between columns)

Return `true` if such a partition exists, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Step 1: Compute Total Sum + Row/Column Sums
- Traverse the grid once to compute:
  - `totalSum` → sum of all elements
  - `rowSum[i]` → sum of each row
  - `colSum[j]` → sum of each column

---

### 🔹 Step 2: Check Feasibility
- If total sum is **odd**, equal partition is impossible:

```
if (totalSum % 2 != 0) → return false
```

---

### 🔹 Step 3: Horizontal Partition (Row-wise)
- Accumulate row sums from top to bottom
- At each step:
```
upperSum == totalSum - upperSum
```
- If true → valid horizontal cut exists

---

### 🔹 Step 4: Vertical Partition (Column-wise)
- Accumulate column sums from left to right
- At each step:
```
leftSum == totalSum - leftSum
```
- If true → valid vertical cut exists

---

## 💻 Implementation

```cpp
class Solution {
public:
    typedef long long ll;

    bool canPartitionGrid(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        vector<ll> rowSum(m, 0);
        vector<ll> colSum(n, 0);

        ll totalSum = 0;

        // Step 1: Compute sums
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                totalSum += grid[i][j];
                rowSum[i] += grid[i][j];
                colSum[j] += grid[i][j];
            }
        }

        // Step 2: Check if partition is possible
        if (totalSum % 2 != 0) return false;

        // Step 3: Horizontal partition
        ll upperSum = 0;
        for (int i = 0; i < m - 1; i++) {
            upperSum += rowSum[i];
            if (upperSum == totalSum - upperSum) {
                return true;
            }
        }

        // Step 4: Vertical partition
        ll leftSum = 0;
        for (int j = 0; j < n - 1; j++) {
            leftSum += colSum[j];
            if (leftSum == totalSum - leftSum) {
                return true;
            }
        }

        return false;
    }
};
```

---

## 📊 Example

### Input
```
grid = [
  [2, 1, 1],
  [1, 1, 2]
]
```

### Total Sum
```
2 + 1 + 1 + 1 + 1 + 2 = 8
target = 4
```

### Horizontal Check
- Row 0 → sum = 4 ✅

### Output
```
true
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`  
  (Single traversal for sums + linear scan)

- **Space Complexity:** `O(m + n)`  
  (Row and column sum arrays)

