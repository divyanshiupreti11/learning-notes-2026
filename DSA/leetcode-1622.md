# ✨ Fancy Sequence – Optimized Implementation 

Implementation of the **Fancy Sequence Data Structure** using **lazy linear transformation and modular arithmetic**.

This solution efficiently supports the following operations:

- `append(val)`
- `addAll(inc)`
- `multAll(m)`
- `getIndex(idx)`

All operations run in **O(1)** time except `append`, which runs in **O(log MOD)** due to modular exponentiation.

---

# 📌 Problem Overview

We maintain a sequence of integers and support four operations:

| Operation | Description |
|--------|-------------|
| `append(val)` | Adds an element to the sequence |
| `addAll(inc)` | Adds `inc` to every element |
| `multAll(m)` | Multiplies every element by `m` |
| `getIndex(idx)` | Returns the element at index `idx` |

A naive approach would require updating the entire array during `addAll` and `multAll`, which would be **O(n)**.

Instead, this solution uses a **lazy linear transformation**.

---

# 🧠 Core Idea

Each element is stored in a **normalized form**.

The actual value is computed using:

```cpp
actual_value = stored_value * mult + add
```

Where:

- `mult` → cumulative multiplication factor  
- `add` → cumulative addition factor

Instead of modifying every element, we update these two variables.

---

# ⚙️ Mathematical Trick

When inserting a new value:

```cpp
val = stored * mult + add
```

Solving for `stored`:

```cpp
stored = (val - add) / mult
```

Since division in modular arithmetic is not allowed, we use **modular inverse**.

```cpp
stored = (val - add) * inverse(mult)
```

Using **Fermat's Little Theorem**:

```cpp
inverse(mult) = mult^(MOD-2) % MOD
```

---
