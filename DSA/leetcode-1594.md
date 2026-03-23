#  📌 Maximum Non Negative Product in a Matrix

## 🧠 Problem Overview
Given a 2D grid of integers (which may include positive, negative, and zero values), find the **maximum non-negative product** of a path from the **top-left corner `(0,0)` to the bottom-right corner `(m-1,n-1)`**.

- You can only move **right** or **down**
- If the maximum product is negative, return `-1`
- Otherwise, return the result modulo `1e9 + 7`

---

## 🚀 Approach

### 🔹 Key Challenge
- The grid contains **negative values**, which can flip signs
- A minimum product can become maximum after multiplying by a negative number

👉 Therefore, we must track:
- **Maximum product**
- **Minimum product**

at each cell

---

### 🔹 Dynamic Programming with Memoization

We use a recursive function with memoization:

```
solve(i, j) → returns {maxProduct, minProduct} from (i, j) to destination
```

---

### 🔹 Transition Logic

From each cell `(i, j)`:
- Move **down** → `(i+1, j)`
- Move **right** → `(i, j+1)`

For both directions:
- Multiply current value with:
  - next cell's max product
  - next cell's min product

Update:
```
maxVal = max(all possible products)
minVal = min(all possible products)
```

---

### 🔹 Base Case
```
If (i, j) == (m-1, n-1):
    return {grid[i][j], grid[i][j]}
```
## 💻 Implementation

```cpp
class Solution {
public:
    int m, n;
    int MOD = 1e9 + 7;

    typedef long long ll;

    vector<vector<pair<ll, ll>>> dp;

    pair<ll, ll> solve(int i, int j, vector<vector<int>>& grid) {
        if (i == m - 1 && j == n - 1) {
            return {grid[i][j], grid[i][j]};
        }

        if (dp[i][j] != make_pair(LLONG_MIN, LLONG_MAX)) {
            return dp[i][j];
        }

        ll maxVal = LLONG_MIN;
        ll minVal = LLONG_MAX;

        // Move Down
        if (i + 1 < m) {
            auto [downMax, downMin] = solve(i + 1, j, grid);

            maxVal = max({maxVal, grid[i][j] * downMax, grid[i][j] * downMin});
            minVal = min({minVal, grid[i][j] * downMax, grid[i][j] * downMin});
        }

        // Move Right
        if (j + 1 < n) {
            auto [rightMax, rightMin] = solve(i, j + 1, grid);

            maxVal = max({maxVal, grid[i][j] * rightMax, grid[i][j] * rightMin});
            minVal = min({minVal, grid[i][j] * rightMax, grid[i][j] * rightMin});
        }

        return dp[i][j] = {maxVal, minVal};
    }

    int maxProductPath(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();

        dp = vector<vector<pair<ll, ll>>>(m, vector<pair<ll, ll>>(n, {LLONG_MIN, LLONG_MAX}));

        auto [maxProd, minProd] = solve(0, 0, grid);

        return (maxProd < 0) ? -1 : maxProd % MOD;
    }
};
```

---

---
