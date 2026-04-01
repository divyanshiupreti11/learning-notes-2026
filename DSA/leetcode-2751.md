# 📌 Robot Collisions
## 🧠 Problem Overview
You are given:

- `positions[]` → positions of robots on a line  
- `healths[]` → health of each robot  
- `directions` → movement direction of each robot (`'L'` or `'R'`)  

### ⚔️ Collision Rules
- Robots moving towards each other collide
- The robot with **lower health is destroyed**
- The robot with **higher health loses 1 health**
- If both have equal health → both are destroyed

Return the **healths of robots that survive**, in the original order.

---

## 🚀 Approach

### 🔹 Step 1: Sort Robots by Position
- We cannot process directly in given order
- Sort robots based on positions to simulate collisions correctly

```
sort indices based on positions
```

---

### 🔹 Step 2: Use Stack for Simulation
- Maintain a stack for robots moving **right (`'R'`)**
- When a robot moving **left (`'L'`)** comes:
  - It may collide with robots in the stack

---

### 🔹 Step 3: Handle Collisions

While stack is not empty:

#### ✅ Case 1: Top robot has higher health
```
health[top] -= 1
current robot dies
```

#### ✅ Case 2: Current robot has higher health
```
health[current] -= 1
top robot dies
```

#### ✅ Case 3: Equal health
```
both die
```

---

### 🔹 Step 4: Collect Survivors
- After simulation, return all robots with `health > 0`

---
