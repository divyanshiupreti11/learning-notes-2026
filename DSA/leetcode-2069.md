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

## 💻 Implementation

```cpp
class Robot {
public:
    int idx = 0;
    bool moved = false;

    vector<vector<int>> pos;

    Robot(int width, int height) {

        // Bottom row (East)
        for (int x = 0; x < width; x++) {
            pos.push_back({x, 0, 0});
        }

        // Right column (North)
        for (int y = 1; y < height; y++) {
            pos.push_back({width - 1, y, 1});
        }

        // Top row (West)
        for (int x = width - 2; x >= 0; x--) {
            pos.push_back({x, height - 1, 2});
        }

        // Left column (South)
        for (int y = height - 2; y > 0; y--) {
            pos.push_back({0, y, 3});
        }

        // Special case: starting point direction
        pos[0][2] = 3;
    }

    void step(int num) {
        moved = true;
        idx = (idx + num) % pos.size();
    }

    vector<int> getPos() {
        return {pos[idx][0], pos[idx][1]};
    }

    string getDir() {
        if (!moved) return "East";

        int d = pos[idx][2];

        if (d == 0) return "East";
        if (d == 1) return "North";
        if (d == 2) return "West";
        return "South";
    }
};
```

---

## 📊 Example

### Input
```
Robot robot = Robot(3, 2);
robot.step(2);
robot.getPos(); → [2, 0]
robot.getDir(); → "East"
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Initialization   | O(width + height) |
| step()           | O(1) |
| getPos()         | O(1) |
| getDir()         | O(1) |

---

## 🎯 Key Insights

- Precomputing the path avoids repeated simulation
- Circular indexing simplifies movement
- Direction is stored along with position

---

## ⚠️ Edge Cases

- `width = 1` or `height = 1`
- Multiple full cycles (`num > perimeter`)
- No movement before calling `getDir()`

---


## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Initialization   | O(width + height) |
| step()           | O(1) |
| getPos()         | O(1) |
| getDir()         | O(1) |

---

## 🎯 Key Insights

- Precomputing the path avoids repeated simulation
- Circular indexing simplifies movement
- Direction is stored along with position

---

## ⚠️ Edge Cases

- `width = 1` or `height = 1`
- Multiple full cycles (`num > perimeter`)
- No movement before calling `getDir()`

---
