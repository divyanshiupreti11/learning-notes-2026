# 📌 Maximum Amount of Money Robot Can Earn
## 🧠 Problem Overview
You are given a 2D grid `coins` where:

- Each cell contains a positive or negative value
- You start from the **top-left corner `(0,0)`**
- You can move only:
  - **Right → `(i, j+1)`**
  - **Down → `(i+1, j)`**

### 🎯 Goal
Maximize the total sum collected while reaching the bottom-right cell.

---

## ⚠️ Special Condition
- You are allowed to **skip up to 2 negative cells**
- Skipping means:
  - You do not add that negative value to your sum

---

## 🚀 Approach

### 🔹 Dynamic Programming + Memoization

We define a recursive function:

```
solve(i, j, k)
```

Where:
- `(i, j)` → current position
- `k` → remaining skips for negative values

---

### 🔹 State Meaning

```
t[i][j][k] = maximum sum achievable from (i, j) to destination
             with k skips remaining
```

---

### 🔹 Base Case

At destination:
```
if coin is negative and skip available:
    return 0
else:
    return coin value
```

---

### 🔹 Transition

#### ✅ Option 1: Take Current Cell
```
take = coins[i][j] + max(
    solve(i+1, j, k),
    solve(i, j+1, k)
)
```

---

#### ✅ Option 2: Skip Current Cell (if negative)
```
if coins[i][j] < 0 and k > 0:
    skip = max(
        solve(i+1, j, k-1),
        solve(i, j+1, k-1)
    )
```

---

### 🔹 Final Decision
```
dp[i][j][k] = max(take, skip)
```

---
