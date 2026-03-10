# 🚀 Find All Possible Stable Binary Arrays II

![LeetCode](https://img.shields.io/badge/LeetCode-Hard-orange)
![Language](https://img.shields.io/badge/Language-C++-blue)
![Technique](https://img.shields.io/badge/Technique-Dynamic%20Programming-green)
![Status](https://img.shields.io/badge/Status-Solved-success)

---

## 📌 Problem Statement

Given three integers:

- `zero` → number of **0s**
- `one` → number of **1s**
- `limit` → maximum allowed **consecutive identical elements**

Return the **number of stable binary arrays** that can be formed using exactly:

- `zero` number of `0`s
- `one` number of `1`s

Such that **no more than `limit` consecutive `0`s or `1`s appear**.

The answer must be returned **modulo \(10^9 + 7\)**.

---

## 🧠 Approach

We solve this problem using **Dynamic Programming**.

### DP State

We define a **3D DP array**
dp[i][j][k]


Where:

- `i` → number of **0s used**
- `j` → number of **1s used**
- `k` → last element placed


k = 0 → array ends with 0
k = 1 → array ends with 1


This allows us to track **valid sequences while maintaining the consecutive limit constraint**.

---

## ⚙️ Initialization

If the array contains only zeros or only ones:


dp[i][0][0] = 1 (if i ≤ limit)
dp[0][j][1] = 1 (if j ≤ limit)


Because sequences like:


000...
111...


are valid only when they **do not exceed the limit**.

---

## 🔄 State Transition

### 1️⃣ Placing `1`

If we add a `1`, the previous element could be `0` or `1`.


dp[i][j][1] =
dp[i][j-1][0] + dp[i][j-1][1]


However, if more than `limit` consecutive `1`s appear, we subtract invalid sequences:


if (j-1 >= limit)
dp[i][j][1] -= dp[i][j-1-limit][0]


---

### 2️⃣ Placing `0`

Similarly for `0`:


dp[i][j][0] =
dp[i-1][j][0] + dp[i-1][j][1]


If the consecutive limit of `0`s is exceeded:


if (i-1 >= limit)
dp[i][j][0] -= dp[i-1-limit][j][1]

