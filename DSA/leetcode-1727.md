# 📌 Largest Submatrix With Rearrangements

## 🧠 Problem Summary
Given a binary matrix (0s and 1s), you can rearrange the columns of each row in any order.  
Return the area of the largest submatrix consisting only of 1s.

---

## 🚀 Approach

### Step 1: Build Heights (Histogram Concept)
Har cell ko upar ke consecutive 1s ka count bana dete hain.  
Agar matrix[i][j] == 1 hai:
matrix[i][j] += matrix[i-1][j]

---

### Step 2: Sort Each Row (Descending)
Har row ko descending order me sort karte hain  
Kyuki columns rearrange kar sakte hain → best width banani hai

---

### Step 3: Calculate Area
Har row ke liye:
area = matrix[i][j] * (j + 1)

Maximum area store karte hain

---
