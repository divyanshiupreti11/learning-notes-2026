# 📌 Decode the Slanted Ciphertext
## 🧠 Problem Overview
You are given:

- A string `encodedText`  
- An integer `rows`  

The string was encoded by writing it in a matrix with `rows` rows and filling it **row-wise**, then reading it **diagonally (top-left → bottom-right)**.

### 🎯 Goal
Reconstruct and return the **original string**.

---

## 🚀 Approach

### 🔹 Step 1: Determine Matrix Dimensions
- Let:
```
columns = encodedText.length() / rows
```

- The matrix has:
  - `rows` rows
  - `columns` columns

---

### 🔹 Step 2: Traverse Diagonally
- Start from each column in the first row
- Move diagonally:
```
index += (columns + 1)
```

- This simulates moving:
  - one row down  
  - one column right  

---

### 🔹 Step 3: Build Original String
- Append characters while traversing diagonally

---

### 🔹 Step 4: Remove Trailing Spaces
- The decoded string may contain extra spaces at the end
- Remove them

---
