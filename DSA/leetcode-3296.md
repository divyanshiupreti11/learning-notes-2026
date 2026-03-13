# ⛰️ Minimum Number of Seconds to Make Mountain Height Zero

## 🧩 Problem
You are given:

- An integer **`mountainHeight`** representing the height of a mountain.
- An array **`workerTimes`**, where `workerTimes[i]` represents the time taken by worker `i` to remove **1 unit** of mountain height.

However, the work is **incremental**:

If a worker removes `k` units of height, the total time taken will be:

t × (1 + 2 + 3 + ... + k)

Which equals:

t × k(k+1)/2

The goal is to **find the minimum number of seconds required** so that all workers together can reduce the mountain height to **0**.

---

# 💡 Approach

### 🔎 Key Observations

- Each worker removes height following a **triangular number pattern**.
- If a worker removes `k` units:
time = t × k(k+1)/2

We need to find the **minimum time** such that the total height removed by all workers ≥ `mountainHeight`.

This suggests using **Binary Search on Time**.

---

# 🚀 Binary Search Strategy

1️⃣ **Search Space**

Minimum time:
1

Maximum time (worst case when slowest worker does all work):
max(workerTimes) × mountainHeight × (mountainHeight + 1) / 2

---

2️⃣ **For a given time `mid`**

Compute how much height each worker can remove.

From:
t × k(k+1)/2 ≤ mid

Solve for `k`.

This becomes a quadratic equation.

Using the derived formula:
k = floor( sqrt(2 × mid / t + 0.25) - 0.5 )
