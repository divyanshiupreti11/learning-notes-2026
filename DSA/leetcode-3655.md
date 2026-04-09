# 📌 XOR After Range Multiplication Queries II
## 🧠 Problem Description

You are given:

- An array `nums`
- A list of queries `queries[][]`

Each query is of the form:
```
[L, R, K, V]
```

### 📌 Query Meaning
For each query:
- Start at index `L`
- Move with step size `K`
- For all indices `i ≤ R`:
```
nums[i] = (nums[i] × V) % (1e9 + 7)
```

---

## 🎯 Objective

After processing all queries, return the **bitwise XOR** of all elements in the final array.

---

## 🚀 Approach

### 🔹 Key Idea: √ Decomposition Optimization

👉 Direct simulation is too slow for small `K`  
👉 We split queries into:

- **Large K (K ≥ √n)** → process directly  
- **Small K (K < √n)** → optimize using prefix technique  

---
## 🔹 Step 1: Handle Large K

For large step size:
```
for (i = L; i <= R; i += K)
    nums[i] *= V
```

👉 Number of updates is small → efficient

---

## 🔹 Step 2: Group Small K Queries

- Store queries based on same `K`
- Process them together using a **difference array**

---

## 🔹 Step 3: Difference Array Trick

Instead of updating each index:

- Apply multiplication at start:
```
diff[L] *= V
```

- Apply inverse at end:
```
diff[next] *= inverse(V)
```

---

## 🔹 Step 4: Prefix Propagation

For same step `K`:
```
diff[i] *= diff[i-K]
```

👉 This spreads updates efficiently

---

## 🔹 Step 5: Apply Updates

```
nums[i] = nums[i] * diff[i]
```

---

## 🔹 Step 6: Compute XOR

```
result = nums[0] ^ nums[1] ^ ... ^ nums[n-1]
```

---

## 💻 Implementation

```cpp
class Solution {
public:
    int M = 1e9 + 7;

    long long power(long long a, long long b) {
        if (b == 0) return 1;

        long long half = power(a, b / 2);
        long long result = (half * half) % M;

        if (b % 2 == 1) {
            result = (result * a) % M;
        }

        return result;
    }

    int xorAfterQueries(vector<int>& nums, vector<vector<int>>& queries) {

        int n = nums.size();
        int blockSize = ceil(sqrt(n));

        unordered_map<int, vector<vector<int>>> smallKMap;

        // Split queries
        for (auto &query : queries) {
            int L = query[0];
            int R = query[1];
            int K = query[2];
            int V = query[3];

            if (K >= blockSize) {
                for (int i = L; i <= R; i += K) {
                    nums[i] = (1LL * nums[i] * V) % M;
                }
            } else {
                smallKMap[K].push_back(query);
            }
        }

        // Process small K queries
        for (auto &[K, allQueries] : smallKMap) {

            vector<long long> diff(n, 1);

            for (auto &query : allQueries) {
                int L = query[0];
                int R = query[1];
                int V = query[3];

                diff[L] = (diff[L] * V) % M;

                int steps = (R - L) / K;
                int next = L + (steps + 1) * K;

                if (next < n) {
                    diff[next] = (diff[next] * power(V, M - 2)) % M;
                }
            }

            // Propagate updates
            for (int i = 0; i < n; i++) {
                if (i - K >= 0) {
                    diff[i] = (diff[i] * diff[i - K]) % M;
                }
            }

            // Apply to nums
            for (int i = 0; i < n; i++) {
                nums[i] = (1LL * nums[i] * diff[i]) % M;
            }
        }

        // Compute XOR
        int result = 0;
        for (int &num : nums) {
            result ^= num;
        }

        return result;
    }
};
```

---

## ⏱️ Complexity Analysis

| Type              | Complexity |
|------------------|-----------|
| Time Complexity  | O(n√n + Q√n) |
| Space Complexity | O(n) |

---

## 🎯 Key Insights

- Split queries based on step size
- Use **modular inverse + prefix propagation**
- Avoid repeated updates for small K

---

## ⚠️ Important Concepts

- Modular exponentiation (Fast Power)
- Modular inverse:
```
inverse(V) = V^(M-2) mod M
```
- Difference array with multiplication

---
## 🏷️ Tags

- Arrays
- Math
- Modular Arithmetic
- Square Root Decomposition
- Optimization
