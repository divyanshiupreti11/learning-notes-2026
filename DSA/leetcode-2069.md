# 🤖 Walking Robot Simulation II
## 🧠 Problem Description

Design a robot that moves along the **perimeter of a rectangular grid** with given dimensions:

- `width`
- `height`

The robot starts at position `(0, 0)` facing **East** and moves along the boundary in a **clockwise direction**.

---

## 🎯 Objective

Implement a class `Robot` with the following functionalities:

- `step(num)` → Move the robot `num` steps forward  
- `getPos()` → Return current position `[x, y]`  
- `getDir()` → Return current direction (`"East"`, `"North"`, `"West"`, `"South"`)  

---

## 🚀 Approach

### 🔹 Key Idea: Precompute Perimeter Path

Instead of simulating movement every time:

👉 Precompute all boundary positions in order and store them in a vector.

Each position stores:
```
[x, y, direction]
```

---

### 🔹 Step 1: Build Perimeter Path

Traverse the rectangle boundary:

1. Bottom row → left to right (East)
2. Right column → bottom to top (North)
3. Top row → right to left (West)
4. Left column → top to bottom (South)

---

### 🔹 Step 2: Maintain Index Pointer

- `idx` → current position index in the path
- Movement is circular:
```
idx = (idx + num) % perimeter_length
```

---

### 🔹 Step 3: Handle Initial Direction Edge Case

- Before any movement → always `"East"`
- After movement → direction based on current position

---
