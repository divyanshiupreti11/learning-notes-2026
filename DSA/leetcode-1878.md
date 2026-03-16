# 🔷 Biggest Three Rhombus Sums in a Grid (C++)

Efficient C++ implementation to find the **three largest distinct rhombus border sums** in a grid.

The algorithm iterates through every cell and treats it as the **top vertex of a rhombus**, then calculates the border sum of all valid rhombuses.

---

# 📌 Problem Overview

Given a 2D grid, a **rhombus** is defined as a diamond-shaped border formed by equal-length diagonals.

The task is to:

- Compute the **sum of elements along the rhombus border**
- Find the **top three largest distinct sums**

---

# 🧠 Approach

For each cell `(i, j)`:

1. Treat the cell as the **top vertex** of a rhombus.
2. Increase the rhombus side length `len`.
3. Ensure the rhombus stays **inside the grid boundaries**.
4. Traverse all **four sides of the rhombus** and compute the border sum.
5. Store sums inside a **set** to maintain **unique values**.
6. Finally return the **largest three values**.

---

# 📐 Rhombus Structure

For a rhombus of side length `len`:

```
      (i, j)
     /     \
(i+len,j-len)   (i+len,j+len)
     \     /
   (i+2len,j)
```

Four borders:

1. Top → Right
2. Right → Bottom
3. Bottom → Left
4. Left → Top
---
  # 💻 C++ Implementation

```cpp
class Solution {
public:
    vector<int> getBiggestThree(vector<vector<int>>& grid) {

        int n = grid.size(), m = grid[0].size();

        set<int> uniqueSum;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){

                // Single cell rhombus
                uniqueSum.insert(grid[i][j]);

                for(int len = 1; i + 2*len < n && j - len >= 0 && j + len < m; len++){

                    int currentSum = 0;

                    // top -> right edge
                    for(int ind = 0; ind < len; ind++)
                        currentSum += grid[i+ind][j+ind];

                    // right -> bottom edge
                    for(int ind = 0; ind < len; ind++)
                        currentSum += grid[i+len+ind][j+len-ind];

                    // bottom -> left edge
                    for(int ind = 0; ind < len; ind++)
                        currentSum += grid[i+2*len-ind][j-ind];

                    // left -> top edge
                    for(int ind = 0; ind < len; ind++)
                        currentSum += grid[i+len-ind][j-len+ind];

                    uniqueSum.insert(currentSum);
                }
            }
        }

        vector<int> ans(uniqueSum.rbegin(), uniqueSum.rend());

        if(ans.size() > 3)
            ans.resize(3);

        return ans;
    }
};
```

---

---

