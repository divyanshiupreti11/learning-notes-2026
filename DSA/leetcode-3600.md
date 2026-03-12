# 🟢  Maximize Spanning Tree Stability with Upgrades

## 📌 Problem

You are given:

- `n` nodes
- `edges` where each edge is represented as:

```
[u, v, w, type]
```

Where:

- `u`, `v` → nodes
- `w` → weight (stability)
- `type`
  - `1` → **must edge**
  - `0` → **flexible edge**

You are also given an integer `k`.

You may **upgrade at most `k` flexible edges**, which doubles their weight.

Your goal is to build a **spanning tree** and **maximize the minimum stability** of any edge in the tree.

If it's impossible to form a spanning tree → return **-1**.

---

# 🧠 Intuition

To maintain connectivity while maximizing stability:

1. **Mandatory edges must be used**.
2. **Flexible edges can optionally be used**.
3. We use **Disjoint Set Union (DSU)** to build the spanning tree.
4. Track flexible edges that help connect components.
5. Use **upgrades on the smallest useful edges** to maximize minimum stability.

---

# ⚙️ Algorithm

### Step 1 — Initialize DSU

Each node starts as its own component.

```
parent[i] = i
size[i] = 1
components = n
```

---

### Step 2 — Separate Edges

Divide edges into:

```
must edges
flex edges
```

---

### Step 3 — Process Must Edges

These edges **must be part of the spanning tree**.

For every must edge:

- Perform union
- Track the **minimum weight**

If union fails → cycle formed → return **-1**

---

### Step 4 — Process Flexible Edges

Sort flexible edges in **descending order of weight**.

Why?

Because we want **stronger edges first** when forming the spanning tree.

If union succeeds:

```
push weight into min heap
```

---

### Step 5 — Use Upgrades

We can upgrade **k edges**.

Upgrade operation:

```
w → 2 * w
```

Apply upgrades to the **smallest useful edges**.

---

### Step 6 — Check Connectivity

If the graph is not fully connected:

```
components != 1 → return -1
```

---
# 💻 C++ Implementation

```cpp
class Solution {
public:
    int components;
    vector<int> parent, size;

    int Union(int u, int v){
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return 0;

        components--;
        if(size[pu] > size[pv]){
            size[pu] += size[pv];
            parent[pv] = pu;
        }
        else{
            size[pv] += size[pu];
            parent[pu] = pv;
        }
        return 1;
    }

    int findParent(int node){
        if(parent[node] == node) return node;
        return parent[node] = findParent(parent[node]);
    }

    int maxStability(int n, vector<vector<int>>& edges, int k) {
        components = n;
        parent.resize(n);
        size.resize(n, 1);

        for(int i = 0; i < n; i++){
            parent[i] = i;
        }

        vector<vector<int>> must, flex;

        for(auto &it : edges){
            if(it[3] == 1) must.push_back(it);
            else flex.push_back(it);
        }

        int mini = INT_MAX;

        for(auto &it : must){
            int u = it[0];
            int v = it[1];
            int w = it[2];

            mini = min(mini, w);

            if(!Union(u, v)){
                return -1;
            }
        }

        sort(flex.begin(), flex.end(), [](vector<int>& a, vector<int>& b){
            return a[2] > b[2];
        });

        priority_queue<int, vector<int>, greater<int>> pq;

        for(auto &it : flex){
            int u = it[0];
            int v = it[1];
            int w = it[2];

            if(Union(u, v)){
                pq.push(w);
            }
        }

        while(k-- && !pq.empty()){
            int x = pq.top();
            pq.pop();
            mini = min(mini, 2 * x);
        }

        if(components != 1) return -1;

        if(!pq.empty()){
            return min(mini, pq.top());
        }

        return mini;
    }
};
```

---

# ⏱ Time Complexity

```
O(E log E)
```

Where:

- `E` = number of edges

Breakdown:

| Operation | Complexity |
|----------|------------|
Sorting edges | O(E log E) |
DSU operations | O(α(n)) |
Priority Queue | O(E log E) |

---

# 💾 Space Complexity

```
O(N + E)
```

Used for:

- DSU arrays
- edge storage
- priority queue

---
