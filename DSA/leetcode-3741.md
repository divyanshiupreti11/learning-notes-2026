
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

---

## 🚀 Key Insight

Since `i < j < k`, the formula simplifies to:

```
distance = 2 × (k - i)
```

👉 Only the **first and third index matter**

---

## 🚀 Approach (Optimized)

### 🔹 Step 1: Track Indices Using HashMap

- Use a map:
```
value → list of indices
```

---

### 🔹 Step 2: Process Array in One Pass

For each index `k`:

- Add index `k` to the list of `nums[k]`
- If the list size becomes ≥ 3:
  - Take last 3 indices:
```
i = vec[size - 3]
k = current index
```

---

### 🔹 Step 3: Compute Distance

```
distance = 2 × (k - i)
```

- Update minimum result

---

### 🔹 Step 4: Return Answer

- If no valid triplet → return `-1`

---
## 💻 Implementation

```cpp
class Solution {
public:
    int minimumDistance(vector<int>& nums) {
        int n = nums.size();

        int result = INT_MAX;

        unordered_map<int, vector<int>> mp;

        for (int k = 0; k < n; k++) {

            mp[nums[k]].push_back(k);

            if (mp[nums[k]].size() >= 3) {

                vector<int> &vec = mp[nums[k]];
                int size = vec.size();

                int i = vec[size - 3];

                result = min(result, 2 * (k - i));
            }
        }

        return (result == INT_MAX) ? -1 : result;
    }
};
```

---
## 📊 Example

### Input
```
nums = [1, 2, 1, 1, 2, 1]
```

### Process
- For value `1` → indices = [0, 2, 3, 5]
- Triplets checked:
  - (0,2,3) → distance = 2 × (3-0) = 6
  - (2,3,5) → distance = 2 × (5-2) = 6

### Output
```
6
```

---
