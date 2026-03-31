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
