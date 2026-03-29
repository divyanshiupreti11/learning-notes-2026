# 📌 Check If Strings Can Be Made Equal
# 🔗 Problem Link
https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-i/description/?envType=daily-question&envId=2026-03-29
## 🧠 Problem Overview
Given two strings `s1` and `s2` of length 4, determine whether `s1` can be made equal to `s2` using any number of swaps between:

- Indices `(0, 2)`
- Indices `(1, 3)`

Return `true` if it is possible, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Key Observation
We can only swap:
- Characters at even indices → `(0, 2)`
- Characters at odd indices → `(1, 3)`

👉 So we only need to check:
- Whether positions `0 & 2` match (in any order)
- Whether positions `1 & 3` match (in any order)

---

### 🔹 Condition Check

#### ✅ Even Indices (0 & 2)
```
(s1[0] == s2[0] && s1[2] == s2[2]) 
OR 
(s1[0] == s2[2] && s1[2] == s2[0])
```

---

#### ✅ Odd Indices (1 & 3)
```
(s1[1] == s2[1] && s1[3] == s2[3]) 
OR 
(s1[1] == s2[3] && s1[3] == s2[1])
```

---

### 🔹 Final Result
```
condition1 && condition2
```

---
## 💻 Implementation

```cpp
class Solution {
public:
    bool canBeEqual(string s1, string s2) {
        bool condition1 =
            (s1[0] == s2[0] && s1[2] == s2[2]) ||
            (s1[0] == s2[2] && s1[2] == s2[0]);

        bool condition2 =
            (s1[1] == s2[1] && s1[3] == s2[3]) ||
            (s1[1] == s2[3] && s1[3] == s2[1]);

        return condition1 && condition2;
    }
};
```

---

## 📊 Example

### Input
```
s1 = "abcd"
s2 = "cdab"
```

### Explanation
- Swap indices (0,2): `"abcd"` → `"cbad"`
- Swap indices (1,3): `"cbad"` → `"cdab"`

### Output
```
true
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(1)`  
- **Space Complexity:** `O(1)`

---
