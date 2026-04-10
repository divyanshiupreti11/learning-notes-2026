# 📌 Minimum Distance Between Three Equal Elements I
## 🔗 Problem Link
https://leetcode.com/problems/minimum-distance-between-three-equal-elements-i/description/?envType=daily-question&envId=2026-04-10
## 🧠 Problem Description

You are given an integer array `nums`.

### 🎯 Objective
Find the **minimum distance** between any triplet `(i, j, k)` such that:

- `i < j < k`
- `nums[i] == nums[j] == nums[k]`

### 📌 Distance Formula
```
distance = |i - j| + |j - k| + |k - i|
```

👉 If no such triplet exists, return `-1`.

---

## 🚀 Approach (Brute Force)

### 🔹 Step 1: Try All Triplets
- Use three nested loops:
  - `i` from `0 → n-1`
  - `j` from `i+1 → n-1`
  - `k` from `j+1 → n-1`

---

### 🔹 Step 2: Check Condition
```
if nums[i] == nums[j] == nums[k]
```

---

### 🔹 Step 3: Compute Distance
```
dist = |i - j| + |j - k| + |k - i|
```

- Keep track of the **minimum distance**

---

### 🔹 Step 4: Return Result
- If no valid triplet found → return `-1`

---
## 💻 Implementation

```cpp
class Solution {
public:
    int minimumDistance(vector<int>& nums) {
        int n = nums.size();
        int ans = INT_MAX;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {

                    if (nums[i] == nums[j] && nums[j] == nums[k]) {

                        int dist = abs(i - j) + abs(j - k) + abs(k - i);
                        ans = min(ans, dist);
                    }
                }
            }
        }

        return (ans == INT_MAX) ? -1 : ans;
    }
};
```

---
## 📊 Example

### Input
```
nums = [1, 2, 1, 1]
```

### Valid Triplet
- Indices: (0, 2, 3)
- Values: (1, 1, 1)

### Distance
```
|0-2| + |2-3| + |3-0| = 2 + 1 + 3 = 6
```

### Output
```
6
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Time Complexity  | O(n³)     |
| Space Complexity | O(1)      |

---
## 🎯 Key Insight

- Since `i < j < k`, the formula simplifies to:
```
distance = 2 × (k - i)
```

👉 Only the **first and last index matter**

---

## ⚠️ Limitations

- Inefficient for large `n`
- Needs optimization using:
  - Hashing
  - Index tracking

---
## 🏷️ Tags

- Arrays
- Brute Force
- Math
- Optimization
