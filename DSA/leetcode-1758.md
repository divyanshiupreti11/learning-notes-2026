#Leetcode 1758 - Minimum Changes To Make Alternating Binary String


## 🔗 Problem Link
https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string/description/?envType=daily-question&envId=2026-03-05

## Problem Description

You are given a binary string `s`.

A string is **alternating** if no two adjacent characters are the same.

Examples of alternating strings:
- `010101`
- `101010`

Your task is to **calculate the minimum number of operations** required to make the string alternating.

In one operation, you can **flip any character**:
- `0 → 1`
- `1 → 0`

## 💡 Key Observation

There are only **two valid alternating patterns** possible:

1️⃣ Start with **0**
010101010...

2️⃣ Start with **1**
101010101...

So we compute how many changes are needed for **both patterns** and take the **minimum**.

---

## 🧠 Approach

1. Traverse the string from index `0` to `n-1`.
2. For each index:
   - If index is **even**
     - Expected char for pattern1 = `0`
     - Expected char for pattern2 = `1`
   - If index is **odd**
     - Expected char for pattern1 = `1`
     - Expected char for pattern2 = `0`

3. Count mismatches for both patterns.
4. Return the minimum operations

5. ## 💻 C++ Implementation


class Solution {
public:
    int minOperations(string s) {
        int n = s.size();
        
        int start_with_0 = 0; // pattern: 010101...
        int start_with_1 = 0; // pattern: 101010...
        
        for(int i = 0; i < n; i++){
            
            if(i % 2 == 0){
                if(s[i] == '0'){
                    start_with_1++;
                } else {
                    start_with_0++;
                }
            }
            else{
                if(s[i] == '1'){
                    start_with_1++;
                } else {
                    start_with_0++;
                }
            }
        }
        
        return min(start_with_0, start_with_1);
    }
};

⏱️ Time Complexity
O(n)

We traverse the string once.

📦 Space Complexity
O(1)

Only two counters are used.

