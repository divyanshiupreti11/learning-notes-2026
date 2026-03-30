#  📌 Check if Strings Can be Made Equal With Operations II
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
