# 🤖 Robot Return to Origin
## 🧠 Problem Description

You are given a string `moves` representing a sequence of movements of a robot on a 2D plane.

Each character in the string represents a direction:
- `'U'` → Move Up
- `'D'` → Move Down
- `'L'` → Move Left
- `'R'` → Move Right

### 🎯 Objective
Determine whether the robot returns to the **origin `(0, 0)`** after executing all the moves.

Return `true` if it does, otherwise return `false`.

---

## 🚀 Approach

### 🔹 Track Coordinates
- Start from origin:
  ```
  (x, y) = (0, 0)
  ```

- For each move:
  - `'U'` → `y + 1`
  - `'D'` → `y - 1`
  - `'L'` → `x - 1`
  - `'R'` → `x + 1`

---

### 🔹 Final Check
- After processing all moves:
  ```
  if (x == 0 && y == 0)
  ```
  → Robot returned to origin ✅

---
