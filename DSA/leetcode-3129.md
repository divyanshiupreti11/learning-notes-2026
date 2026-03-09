# 🔄 Number of Stable Arrays

## 📌 Problem Statement

You are given three integers:

- `zero` — the number of `0`s
- `one` — the number of `1`s
- `limit` — the maximum number of identical elements allowed consecutively

Your task is to determine the **number of stable arrays** that can be formed using exactly `zero` zeros and `one` ones.

A **stable array** is defined as an array in which **no more than `limit` identical elements appear consecutively**.

Since the number of possible arrays can be very large, return the result **modulo \(10^9 + 7\)**.

---

## 🧠 Intuition

A brute-force approach would attempt to generate all possible arrays containing `zero` zeros and `one` ones. However, the number of such arrays grows exponentially and becomes computationally infeasible.

Instead, we use **Dynamic Programming (DP)** to build the solution incrementally while keeping track of:

- the number of zeros used
- the number of ones used
- the last element placed in the array

Tracking the last element ensures that the **consecutive limit constraint** is not violated.

---

## 📝 Dynamic Programming Approach

We maintain a **3-dimensional DP table**:
dp[ones][zeros][last]

### State Definition

| State | Description |
|------|-------------|
| `dp[i][j][0]` | Number of ways to form an array using `i` ones and `j` zeros where the **last element is 0** |
| `dp[i][j][1]` | Number of ways to form an array using `i` ones and `j` zeros where the **last element is 1** |

---

## 📊 Transition

### Case 1: Last element is `1`

If the last element is `1`, the previous block must consist of zeros.

We try all possible lengths of consecutive zeros:

len = 1 → min(limit, zeros)

Transition:

dp[ones][zeros][1] += dp[ones][zeros - len][0]

---

### Case 2: Last element is `0`

If the last element is `0`, the previous block must consist of ones.
len = 1 → min(limit, ones)

Transition:
dp[ones][zeros][0] += dp[ones - len][zeros][1]

---

## Base Case
dp[0][0][0] = 1
dp[0][0][1] = 1


This represents the starting configuration before placing any elements.

---

## Final Result

The final array may end with either `0` or `1`, so the answer is:


answer = dp[one][zero][0] + dp[one][zero][1]


The result is returned modulo \(10^9 + 7\).

---

---

## 💻 C++ Implementation

```cpp
class Solution {
public:
    int M = 1e9+7;
    int t[201][201][2];

    int numberOfStableArrays(int zero, int one, int limit) {

        memset(t,0,sizeof(t));

        t[0][0][0] = 1;
        t[0][0][1] = 1;

        for(int onesLeft = 0; onesLeft <= one; onesLeft++){
            for(int zerosLeft = 0; zerosLeft <= zero; zerosLeft++){

                if(onesLeft==0 && zerosLeft==0) continue;

                int result = 0;

                for(int len=1; len<=min(zerosLeft,limit); len++){
                    result = (result + t[onesLeft][zerosLeft-len][0]) % M;
                }

                t[onesLeft][zerosLeft][1] = result;

                result = 0;

                for(int len=1; len<=min(onesLeft,limit); len++){
                    result = (result + t[onesLeft-len][zerosLeft][1]) % M;
                }

                t[onesLeft][zerosLeft][0] = result;
            }
        }

        int startWithOne = t[one][zero][0];
        int startWithZero = t[one][zero][1];

        return (startWithOne + startWithZero) % M;
    }
};
```

## ⏰ Complexity Analysis

### Time Complexity


O(zero × one × limit)


### Space Complexity


O(zero × one)
