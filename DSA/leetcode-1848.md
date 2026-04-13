# 📌 Minimum Distance to the Target Element

## 🧠 Problem Description

You are given:

- An integer array `nums`
- An integer `target`
- An integer `start` representing a starting index

### 🎯 Objective
Find the **minimum distance** between the `start` index and any index `i` such that:

```
nums[i] == target
```

### 📌 Distance Definition
```
distance = |i - start|
```

---

## 🚀 Approach

### 🔹 Step 1: Traverse the Array
- Iterate through all indices of the array

---

### 🔹 Step 2: Check for Target
- If:
```
nums[i] == target
```
- Compute:
```
distance = abs(i - start)
```

---

### 🔹 Step 3: Track Minimum Distance
- Maintain a variable `minDistance`
- Update it whenever a smaller distance is found

---

### 🔹 Step 4: Return Result
- Return the minimum distance found

---
## 💻 Implementation

```cpp
class Solution {
public:
    int getMinDistance(vector<int>& nums, int target, int start) {
        int n = nums.size();

        int minDistance = INT_MAX;

        for (int i = 0; i < n; i++) {
            if (nums[i] == target) {
                minDistance = min(minDistance, abs(i - start));
            }
        }

        return minDistance;
    }
};
```
## 📊 Example

### Input
```
nums = [1, 2, 3, 4, 5]
target = 5
start = 3
```

### Valid Indices
- Target found at index `4`

### Distance
```
|4 - 3| = 1
```

### Output
```
1
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Time Complexity  | O(n)      |
| Space Complexity | O(1)      |

---

## 🎯 Key Insights

- A simple linear scan is sufficient
- Absolute difference ensures correct distance
- No need for sorting or extra data structures

---

## ⚠️ Edge Cases

- Target appears multiple times → choose closest
- Target at `start` index → distance = 0
- Large array → still efficient

---
## 🏷️ Tags

- Arrays
- Linear Search
- Simulation
