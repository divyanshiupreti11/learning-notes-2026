# ⛰️ Minimum Number of Seconds to Make Mountain Height Zero
## 🔗 Problem Link
https://leetcode.com/problems/minimum-number-of-seconds-to-make-mountain-height-zero/description/?envType=daily-question&envId=2026-03-13

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


---

3️⃣ **Check Condition**

If total removable height ≥ `mountainHeight`

✔ Possible → search smaller time  
❌ Not possible → search larger time

---

# 🧠 Algorithm

1. Binary search on time.
2. For each `mid`, calculate removable height using all workers.
3. If removable height ≥ mountainHeight → update answer.
4. Continue until minimum valid time is found.

---

# 🧾 Code (C++)

```cpp
class Solution {
public:
typedef long long ll;

    bool check(ll mid, vector<int>& workerTimes, int mH) {
        ll h = 0;

        for(int &t : workerTimes) {

            h += (ll)(sqrt(2.0 * mid / t + 0.25) - 0.5);

            if(h >= mH) {
                return true;
            }
        }

        return h >= mH;
    }

    long long minNumberOfSeconds(int mountainHeight, vector<int>& workerTimes) {

        int maxTime = *max_element(begin(workerTimes), end(workerTimes));

        ll l = 1;
        ll r = (ll)maxTime * mountainHeight * (mountainHeight + 1) / 2;

        ll result = 0;

        while(l <= r) {

            ll mid = l + (r - l) / 2;

            if(check(mid, workerTimes, mountainHeight)) {
                result = mid;
                r = mid - 1;
            }
            else {
                l = mid + 1;
            }
        }

        return result;
    }
};
```
---
### ⏱️ Time Complexity

Binary Search runs on the time range.

Each check iterates through all workers.

**Overall Time Complexity**
O(n log(max(workerTimes) × mountainHeight²))
Where:
- `n` = number of workers



### 🧠 Space Complexity


O(1)
