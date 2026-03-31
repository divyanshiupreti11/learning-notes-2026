# 📌 Lexicographically Smallest Generated String
## 🧠 Problem Overview
You are given two strings:

- `str1` → a binary constraint string consisting of `'T'` and `'F'`
- `str2` → a pattern string

Your task is to construct a string `word` such that:

- For every index `i`:
  - If `str1[i] == 'T'` → substring starting at `i` must match `str2`
  - If `str1[i] == 'F'` → substring starting at `i` must **not** match `str2`

Return the constructed string if possible, otherwise return an empty string `""`.

---

## 🚀 Approach

### 🔹 Step 1: Initialize Result String
- Let:
```
N = n + m - 1
```
- Create a string `word` of size `N` initialized with placeholder `$`

---

### 🔹 Step 2: Handle 'T' Constraints (Force Matching)
For every index `i` where `str1[i] == 'T'`:

- Place `str2` starting at index `i`
- If conflict occurs → return `""`

```
word[i + j] = str2[j]
```

---

### 🔹 Step 3: Fill Remaining Characters
- Replace all `$` with `'a'`
- Mark these positions as changeable using `canChange[]`

---

### 🔹 Step 4: Handle 'F' Constraints (Avoid Matching)

For every index `i` where `str1[i] == 'F'`:

- If substring matches `str2`:
  - Modify at least one character in that range
  - Prefer changing from right to left
  - Change only positions marked as changeable

- If no change is possible → return `""`

---

### 🔹 Helper Function

Check if substring matches:
```
isSame(word, str2, i, m)
```

---

## 💻 Implementation

```cpp
class Solution {
public:

    bool isSame(string &word, string &str2, int i, int m) {
        for (int j = 0; j < m; j++) {
            if (word[i] != str2[j]) return false;
            i++;
        }
        return true;
    }

    string generateString(string str1, string str2) {
        int n = str1.length();
        int m = str2.length();

        int N = n + m - 1;

        string word(N, '$');
        vector<bool> canChange(N, false);

        // Step 1: Apply 'T' constraints
        for (int i = 0; i < n; i++) {
            if (str1[i] == 'T') {
                int idx = i;
                for (int j = 0; j < m; j++) {
                    if (word[idx] != '$' && word[idx] != str2[j]) {
                        return "";
                    }
                    word[idx] = str2[j];
                    idx++;
                }
            }
        }

        // Step 2: Fill remaining characters
        for (int i = 0; i < N; i++) {
            if (word[i] == '$') {
                word[i] = 'a';
                canChange[i] = true;
            }
        }

        // Step 3: Handle 'F' constraints
        for (int i = 0; i < n; i++) {
            if (str1[i] == 'F') {
                if (isSame(word, str2, i, m)) {

                    bool changed = false;

                    for (int k = i + m - 1; k >= i; k--) {
                        if (canChange[k]) {
                            word[k] = 'b';
                            changed = true;
                            break;
                        }
                    }

                    if (!changed) return "";
                }
            }
        }

        return word;
    }
};
```

---

## 📊 Example

### Input
```
str1 = "TFT"
str2 = "ab"
```

### Explanation
- At index 0 → must match `"ab"`
- At index 1 → must NOT match `"ab"`
- At index 2 → must match `"ab"`

The algorithm constructs a valid string satisfying all constraints.

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n × m)`  
- **Space Complexity:** `O(n + m)`

---
