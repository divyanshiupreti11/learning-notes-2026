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
## 💻 Implementation

```cpp
class Solution {
public:
    int robotSim(vector<int>& commands, vector<vector<int>>& obstacles) {

        unordered_set<string> st;

        // Store obstacles
        for (vector<int>& obs : obstacles) {
            string key = to_string(obs[0]) + "_" + to_string(obs[1]);
            st.insert(key);
        }

        int x = 0, y = 0;
        int maxDist = 0;

        // Initial direction: North
        pair<int, int> dir = {0, 1};

        for (int cmd : commands) {

            if (cmd == -2) {
                // Turn left
                dir = {-dir.second, dir.first};
            }
            else if (cmd == -1) {
                // Turn right
                dir = {dir.second, -dir.first};
            }
            else {
                // Move forward
                for (int step = 0; step < cmd; step++) {
                    int newX = x + dir.first;
                    int newY = y + dir.second;

                    string key = to_string(newX) + "_" + to_string(newY);

                    // Stop if obstacle found
                    if (st.count(key)) break;

                    x = newX;
                    y = newY;
                }
            }

            maxDist = max(maxDist, x * x + y * y);
        }

        return maxDist;
    }
};
```

---

## 📊 Example

### Input
```
commands = [4, -1, 3]
obstacles = []
```

### Execution
- Move 4 steps north → (0,4)
- Turn right → facing east
- Move 3 steps → (3,4)

### Output
```
25
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Time Complexity  | O(n + k)  |
| Space Complexity | O(k)      |

Where:
- `n` = number of commands  
- `k` = number of obstacles  

---

## 🎯 Key Insights

- Use **hashing** for constant-time obstacle lookup
- Simulate movement step-by-step
- Direction rotation is handled using vector transformation

---

## ⚠️ Edge Cases

- No obstacles → free movement
- Obstacles immediately in front
- Large coordinates
- Multiple turns without movement


