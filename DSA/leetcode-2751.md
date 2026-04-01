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
## 💻 Implementation

```cpp
class Solution {
public:
    vector<int> survivedRobotsHealths(vector<int>& positions, vector<int>& healths, string directions) {
        int n = positions.size();

        vector<int> indices(n);
        iota(indices.begin(), indices.end(), 0);

        // Sort robots by position
        sort(indices.begin(), indices.end(), [&](int &i, int &j) {
            return positions[i] < positions[j];
        });

        stack<int> st;

        for (int &currIdx : indices) {

            if (directions[currIdx] == 'R') {
                st.push(currIdx);
            } else {
                // Handle collisions
                while (!st.empty() && healths[currIdx] > 0) {
                    int topIdx = st.top();
                    st.pop();

                    if (healths[topIdx] > healths[currIdx]) {
                        healths[topIdx] -= 1;
                        healths[currIdx] = 0;
                        st.push(topIdx);
                    } 
                    else if (healths[topIdx] < healths[currIdx]) {
                        healths[currIdx] -= 1;
                        healths[topIdx] = 0;
                    } 
                    else {
                        healths[currIdx] = 0;
                        healths[topIdx] = 0;
                    }
                }
            }
        }

        vector<int> result;

        for (int i = 0; i < n; i++) {
            if (healths[i] > 0) {
                result.push_back(healths[i]);
            }
        }

        return result;
    }
};
```

---
