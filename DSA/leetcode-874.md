# 🤖 Walking Robot Simulation

## 🧠 Problem Description

You are given:

- `commands[]` → a list of movement instructions  
- `obstacles[][]` → positions of obstacles on a 2D grid  

The robot starts at position `(0, 0)` facing **north**.

---

## 🚦 Movement Rules

Each command represents:

- `-2` → Turn left (90°)
- `-1` → Turn right (90°)
- `1 to 9` → Move forward by given steps

---

## ⚠️ Obstacle Constraint

- If the robot encounters an obstacle:
  - It **stops before hitting it**
  - Continues with the next command

---

## 🎯 Objective

Return the **maximum Euclidean distance squared** from the origin `(0,0)` that the robot reaches at any point.

```
distance = x² + y²
```

---

## 🚀 Approach

### 🔹 Step 1: Store Obstacles Efficiently
- Use a hash set to store obstacle positions
- Represent each position as a string:
```
"x_y"
```

---

### 🔹 Step 2: Direction Handling

We represent direction as a vector:
```
(0, 1) → North
```

#### Turning Logic:
- Left turn:
```
(x, y) → (-y, x)
```
- Right turn:
```
(x, y) → (y, -x)
```

---

### 🔹 Step 3: Process Commands

For each command:

#### ✅ Turn Commands
- Update direction vector accordingly

#### ✅ Move Commands
- Move step-by-step
- At each step:
  - Check if next position is an obstacle
  - If yes → stop movement

---

### 🔹 Step 4: Track Maximum Distance
- After each command:
```
maxDistance = max(maxDistance, x² + y²)
```

---
