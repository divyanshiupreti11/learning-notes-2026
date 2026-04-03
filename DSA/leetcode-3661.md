# 📌 Maximum Walls Destroyed by Robots


## 🧠 Problem Overview
You are given:

- `robots[]` → positions of robots  
- `distance[]` → maximum distance each robot can cover  
- `walls[]` → positions of walls  

### 🎯 Goal
Each robot can destroy walls either:
- To the **left**, or  
- To the **right**

👉 Find the **maximum number of walls** that can be destroyed.

---

## ⚠️ Constraints

- Robots cannot overlap their effective ranges
- Each robot must choose **only one direction** (left or right)
- Walls must be counted **only once**

---

## 🚀 Approach

### 🔹 Step 1: Preprocessing

#### ✅ Pair Robots with Distance
```
(roboDist[i] = {position, distance})
```

#### ✅ Sort Robots
- Sort robots by position to handle overlapping constraints

#### ✅ Sort Walls
- Helps in efficient counting using binary search

---

### 🔹 Step 2: Define Valid Range for Each Robot

For each robot:

```
L = max(position - distance, left boundary)
R = min(position + distance, right boundary)
```

- Boundaries ensure no overlap with adjacent robots

---

### 🔹 Step 3: Count Walls Using Binary Search

Efficiently count walls in range `[l, r]`:

```
count = upper_bound(r) - lower_bound(l)
```

---

### 🔹 Step 4: Dynamic Programming (Recursion + Memoization)

Define:
```
solve(i, prevDir)
```

Where:
- `i` → current robot index
- `prevDir` → direction of previous robot
  - `0` → left
  - `1` → right

---

### 🔹 Transitions

#### ✅ Option 1: Move Left
```
leftWalls + solve(i+1, 0)
```

- Adjust range if previous robot moved right

---

#### ✅ Option 2: Move Right
```
rightWalls + solve(i+1, 1)
```

---

### 🔹 Final Answer
```
max(leftTake, rightTake)
```

---


---


## 💻 Implementation

```cpp
class Solution {
public:
    typedef pair<int,int> P;

    vector<vector<int>> dp;

    // Count walls in range [l, r]
    int countWalls(vector<int>& walls, int l, int r) {
        int left = lower_bound(walls.begin(), walls.end(), l) - walls.begin();
        int right = upper_bound(walls.begin(), walls.end(), r) - walls.begin();
        return right - left;
    }

    int solve(vector<int>& walls, vector<P>& robots, vector<P>& range, int i, int prevDir) {
        if (i == robots.size()) return 0;

        if (dp[i][prevDir] != -1) return dp[i][prevDir];

        int leftStart = range[i].first;

        // Adjust if previous robot moved right
        if (prevDir == 1) {
            leftStart = max(leftStart, range[i - 1].second + 1);
        }

        int leftTake = countWalls(walls, leftStart, robots[i].first)
                     + solve(walls, robots, range, i + 1, 0);

        int rightTake = countWalls(walls, robots[i].first, range[i].second)
                      + solve(walls, robots, range, i + 1, 1);

        return dp[i][prevDir] = max(leftTake, rightTake);
    }

    int maxWalls(vector<int>& robots, vector<int>& distance, vector<int>& walls) {
        int n = robots.size();

        vector<P> roboDist(n);
        for (int i = 0; i < n; i++) {
            roboDist[i] = {robots[i], distance[i]};
        }

        sort(roboDist.begin(), roboDist.end());
        sort(walls.begin(), walls.end());

        // Compute valid ranges
        vector<P> range(n);

        for (int i = 0; i < n; i++) {
            int pos = roboDist[i].first;
            int d = roboDist[i].second;

            int leftLimit = (i == 0) ? 1 : roboDist[i - 1].first + 1;
            int rightLimit = (i == n - 1) ? 1e9 : roboDist[i + 1].first - 1;

            int L = max(pos - d, leftLimit);
            int R = min(pos + d, rightLimit);

            range[i] = {L, R};
        }

        dp.assign(n + 1, vector<int>(2, -1));

        return solve(walls, roboDist, range, 0, 0);
    }
};
```

---

## 📊 Example

### Input
```
robots   = [2, 6]
distance = [2, 2]
walls    = [1, 3, 5, 7]
```

### Explanation
- Robot at 2 → range [1,4]
- Robot at 6 → range [4,8]
- Choose optimal directions to maximize wall destruction

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n log n + n × log w)`  
  - Sorting + binary search

- **Space Complexity:** `O(n)`  
  - DP table

---

## 🎯 Key Insight

- Split problem into independent robot decisions
- Use binary search for fast wall counting
- DP ensures optimal global decision

---

## ⚠️ Edge Cases

- Overlapping ranges between robots
- No walls in range
- Single robot case

---
## 🏷️ Tags
- Dynamic Programming
- Binary Search
- Greedy
- Sorting
- Simulation
