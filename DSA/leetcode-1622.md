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
# 💻 C++ Implementation

```cpp
class Fancy {
public:
    typedef long long ll;

    ll MOD = 1e9 + 7;
    vector<ll> seq;

    ll add = 0;
    ll mult = 1;

    long long power(long long a, long long b) {
        if (b == 0) return 1;

        long long half = power(a, b / 2);

        long long result = (half * half) % MOD;

        if (b % 2 == 1)
            result = (result * a) % MOD;

        return result;
    }

    Fancy() {}

    void append(int val) {
        long long x = ((val - add) % MOD + MOD) % MOD;
        x = (x * power(mult, MOD - 2)) % MOD;

        seq.push_back(x);
    }

    void addAll(int inc) {
        add = (add + inc) % MOD;
    }

    void multAll(int m) {
        mult = (mult * m) % MOD;
        add = (add * m) % MOD;
    }

    int getIndex(int idx) {
        if (idx >= seq.size()) return -1;

        return (seq[idx] * mult + add) % MOD;
    }
};
```

---

# 📊 Time Complexity

| Operation | Complexity |
|----------|-----------|
| `append` | O(log MOD) |
| `addAll` | O(1) |
| `multAll` | O(1) |
| `getIndex` | O(1) |

---

# 🚀 Key Concepts Used

- Modular Arithmetic
- Fast Exponentiation
- Modular Inverse
- Lazy Updates
- Linear Transformation

---
