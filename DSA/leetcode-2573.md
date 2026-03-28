# 📌  Find the String with LCP
## 🧠 Problem Overview
You are given a 2D matrix `lcp` where:

- `lcp[i][j]` represents the **length of the longest common prefix** between the suffixes of a string `word` starting at indices `i` and `j`

Your task is to:

- Construct a valid string `word` that satisfies the given `lcp` matrix  
- If no such string exists, return an empty string `""`

---

## 🚀 Approach

### 🔹 Step 1: Understand LCP Matrix
- `lcp[i][j] > 0` → `word[i] == word[j]`
- `lcp[i][j] == 0` → `word[i] != word[j]`

---

### 🔹 Step 2: Construct the String Greedily

We build the string character by character:

#### ✅ Case 1: Matching Prefix Exists
- If there exists some `j < i` such that:
```
lcp[j][i] > 0
```
- Then:
```
word[i] = word[j]
```

---

#### ✅ Case 2: Assign New Character
- If no such `j` exists:
  - Track forbidden characters from previous positions where:
```
lcp[j][i] == 0
```
- Assign the smallest valid character (`'a'` to `'z'`) not forbidden

---

#### ❌ Failure Case
- If no valid character can be assigned → return `""`

---

### 🔹 Step 3: Validate Using LCP Construction

After constructing the string:

- Rebuild the LCP matrix using the string
- Compare with the given matrix
- If mismatch → return `""`

---
