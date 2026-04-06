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

