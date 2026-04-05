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
## 💻 Implementation

```cpp
class Solution {
public:
    bool judgeCircle(string moves) {
        int x = 0;
        int y = 0;

        for (char &ch : moves) {
            if (ch == 'U') y++;
            else if (ch == 'D') y--;
            else if (ch == 'L') x--;
            else if (ch == 'R') x++;
        }

        return x == 0 && y == 0;
    }
};
```

---
## 📊 Example

### Input
```
moves = "UDLR"
```

### Execution
- U → (0,1)
- D → (0,0)
- L → (-1,0)
- R → (0,0)

### Output
```
true
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Time Complexity  | O(n)      |
| Space Complexity | O(1)      |

---

## 🎯 Key Insights

- Only the final position matters, not the path
- Equal number of opposite moves cancel each other:
  - U cancels D
  - L cancels R

---

## ⚠️ Edge Cases

- Empty string → returns `true`
- Only one direction → returns `false`
- Large input size → handled efficiently in linear time

---
