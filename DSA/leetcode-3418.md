# 📌 Maximum Amount of Money Robot Can Earn
## 🧠 Problem Overview
You are given a 2D grid `coins` where:

- Each cell contains a positive or negative value
- You start from the **top-left corner `(0,0)`**
- You can move only:
  - **Right → `(i, j+1)`**
  - **Down → `(i+1, j)`**

### 🎯 Goal
Maximize the total sum collected while reaching the bottom-right cell.

---

## ⚠️ Special Condition
- You are allowed to **skip up to 2 negative cells**
- Skipping means:
  - You do not add that negative value to your sum

---

## 🚀 Approach

### 🔹 Dynamic Programming + Memoization

We define a recursive function:

```
solve(i, j, k)
```

Where:
- `(i, j)` → current position
- `k` → remaining skips for negative values

---

### 🔹 State Meaning

```
t[i][j][k] = maximum sum achievable from (i, j) to destination
             with k skips remaining
```

---

### 🔹 Base Case

At destination:
```
if coin is negative and skip available:
    return 0
else:
    return coin value
```

---

### 🔹 Transition

#### ✅ Option 1: Take Current Cell
```
take = coins[i][j] + max(
    solve(i+1, j, k),
    solve(i, j+1, k)
)
```

---

#### ✅ Option 2: Skip Current Cell (if negative)
```
if coins[i][j] < 0 and k > 0:
    skip = max(
        solve(i+1, j, k-1),
        solve(i, j+1, k-1)
    )
```

---

### 🔹 Final Decision
```
dp[i][j][k] = max(take, skip)
```

---
## 💻 Implementation

```cpp
class Solution {
public:
    int m, n;
    int t[501][501][3];

    int solve(vector<vector<int>>& coins, int i, int j, int k) {

        if (i == m - 1 && j == n - 1) {
            if (coins[i][j] < 0 && k > 0) return 0;
            return coins[i][j];
        }

        if (i >= m || j >= n) return INT_MIN;

        if (t[i][j][k] != INT_MIN) {
            return t[i][j][k];
        }

        // Option 1: Take current cell
        int take = coins[i][j] + max(
            solve(coins, i + 1, j, k),
            solve(coins, i, j + 1, k)
        );

        // Option 2: Skip current cell
        int skip = INT_MIN;

        if (coins[i][j] < 0 && k > 0) {
            int down = solve(coins, i + 1, j, k - 1);
            int right = solve(coins, i, j + 1, k - 1);
            skip = max(down, right);
        }

        return t[i][j][k] = max(take, skip);
    }

    int maximumAmount(vector<vector<int>>& coins) {
        m = coins.size();
        n = coins[0].size();

        // Initialize DP
        for (int i = 0; i < 501; i++) {
            for (int j = 0; j < 501; j++) {
                for (int k = 0; k < 3; k++) {
                    t[i][j][k] = INT_MIN;
                }
            }
        }

        return solve(coins, 0, 0, 2);
    }
};
```

---
## 📊 Example

### Input
```
coins = [
  [1, -2, 3],
  [4, -5, 6],
  [7, 8, 9]
]
```

### Explanation
- You can skip up to 2 negative values
- Best path avoids maximum loss

### Output
```
Maximum sum path with optimal skips
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n × k)`  
  (Each state computed once)

- **Space Complexity:** `O(m × n × k)`  
  (3D DP array)

---

