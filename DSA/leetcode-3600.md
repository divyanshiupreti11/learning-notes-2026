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
