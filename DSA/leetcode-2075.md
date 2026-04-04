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
## 💻 Implementation

```cpp
class Solution {
public:
    string decodeCiphertext(string encodedText, int rows) {
        int length = encodedText.length();

        int columns = length / rows;

        string originalText;

        // Traverse diagonally
        for (int col = 0; col < columns; col++) {
            for (int idx = col; idx < length; idx += (columns + 1)) {
                originalText += encodedText[idx];
            }
        }

        // Remove trailing spaces
        while (!originalText.empty() && originalText.back() == ' ') {
            originalText.pop_back();
        }

        return originalText;
    }
};
```

---
## 📊 Example

### Input
```
encodedText = "ch   ie   pr"
rows = 3
```

### Matrix Representation
```
c h    
i e    
p r    
```

### Diagonal Traversal
```
c → e → r  
h →    
i → p  
```

### Output
```
"cipher"
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(n)`  

---

## 🎯 Key Insight

- Diagonal traversal corresponds to index jump of `(columns + 1)`
- No need to explicitly build the matrix

---

## ⚠️ Edge Cases

- `rows = 1` → return original string
- Empty string
- Trailing spaces in encoded text

---
