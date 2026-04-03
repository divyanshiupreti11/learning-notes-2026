# 📌 Maximum Walls Destroyed by Robots


## 🧠 Problem Overview
You are given:

- `robots[]` → positions of robots  
- `distance[]` → maximum distance each robot can cover  
- `walls[]` → positions of walls  

### 🎯 Goal
Each robot can destroy walls either:
- To the **left**, or  
- To the **right**

👉 Find the **maximum number of walls** that can be destroyed.

---

## ⚠️ Constraints

- Robots cannot overlap their effective ranges
- Each robot must choose **only one direction** (left or right)
- Walls must be counted **only once**

---

## 🚀 Approach

### 🔹 Step 1: Preprocessing

#### ✅ Pair Robots with Distance
```
(roboDist[i] = {position, distance})
```

#### ✅ Sort Robots
- Sort robots by position to handle overlapping constraints

#### ✅ Sort Walls
- Helps in efficient counting using binary search

---

### 🔹 Step 2: Define Valid Range for Each Robot

For each robot:

```
L = max(position - distance, left boundary)
R = min(position + distance, right boundary)
```

- Boundaries ensure no overlap with adjacent robots

---

### 🔹 Step 3: Count Walls Using Binary Search

Efficiently count walls in range `[l, r]`:

```
count = upper_bound(r) - lower_bound(l)
```

---

### 🔹 Step 4: Dynamic Programming (Recursion + Memoization)

Define:
```
solve(i, prevDir)
```

Where:
- `i` → current robot index
- `prevDir` → direction of previous robot
  - `0` → left
  - `1` → right

---

### 🔹 Transitions

#### ✅ Option 1: Move Left
```
leftWalls + solve(i+1, 0)
```

- Adjust range if previous robot moved right

---

#### ✅ Option 2: Move Right
```
rightWalls + solve(i+1, 1)
```

---

### 🔹 Final Answer
```
max(leftTake, rightTake)
```

---


---

## 🏷️ Tags
- Dynamic Programming
- Binary Search
- Greedy
- Sorting
- Simulation
