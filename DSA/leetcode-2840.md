#  📌 Check if Strings Can be Made Equal With Operations II
## 🔗 Problem Link
https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-ii/description/?envType=daily-question&envId=2026-03-30
## 🧠 Problem Overview
Given two strings `s1` and `s2` of equal length, determine whether they can be made equal by performing any number of swaps such that:

- You can swap characters only among:
  - **Even indices** with even indices
  - **Odd indices** with odd indices

Return `true` if the strings can be made equal, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Key Observation
- Characters at **even positions** can only move within even positions  
- Characters at **odd positions** can only move within odd positions  

👉 So we must ensure:
- Frequency of characters at even indices in `s1` == `s2`
- Frequency of characters at odd indices in `s1` == `s2`

---

### 🔹 Frequency Counting

We maintain two frequency arrays:

- `even[26]` → tracks characters at even indices  
- `odd[26]` → tracks characters at odd indices  

---

### 🔹 Process

For each index `i`:

- If `i` is even:
  - Increment count for `s1[i]`
  - Decrement count for `s2[i]`

- If `i` is odd:
  - Increment count for `s1[i]`
  - Decrement count for `s2[i]`

---

### 🔹 Validation
- After processing all characters:
  - If all values in both arrays are `0` → valid
  - Otherwise → not possible

---
## 💻 Implementation

```cpp
class Solution {
public:
    bool checkStrings(string s1, string s2) {
        int even[26] = {0};
        int odd[26] = {0};

        int n = s1.length();

        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                even[s1[i] - 'a']++;
                even[s2[i] - 'a']--;
            } else {
                odd[s1[i] - 'a']++;
                odd[s2[i] - 'a']--;
            }
        }

        for (int i = 0; i < 26; i++) {
            if (even[i] != 0 || odd[i] != 0) {
                return false;
            }
        }

        return true;
    }
};
```

---

## 📊 Example

### Input
```
s1 = "abcdba"
s2 = "cabdab"
```

### Explanation
- Even indices characters match in frequency  
- Odd indices characters also match in frequency  

### Output
```
true
```

---
## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(1)`  
  (Fixed-size arrays of 26 characters)

---
