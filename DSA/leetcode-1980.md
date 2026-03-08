
# 🔢 Find Unique Binary String (LeetCode 1980)
# 🔗 Problem Link
https://leetcode.com/problems/find-unique-binary-string/description/?envType=daily-question&envId=2026-03-08

## 📌 Problem Statement

Given an array `nums` containing **n unique binary strings**, each of length `n`, return **any binary string of length `n` that does not appear in `nums`**.

Each string consists only of characters:
'0' and '1'

The returned binary string must be **different from every string in the input array**.

---

## 📥 Example

### Example 1
Input: nums = ["01","10"]
Output: "00"

Explanation:

Possible binary strings of length 2:
00
01
10
11

Since `"01"` and `"10"` are already in the array, `"00"` or `"11"` can be returned.

---

# 💡 Key Idea (Cantor's Diagonalization Trick)

This problem can be solved using a famous concept called:

Cantor's Diagonalization

The idea is simple:

1. Look at the **i-th string**
2. Take the **i-th character** from that string
3. Flip the bit
0 → 1
1 → 0

This guarantees that the new string will **differ from every string in the array at least at one position**.

Thus, the generated string **cannot exist in the input list**.

---

# 🧠 Intuition

Suppose the input is: nums = ["111","011","001"]
Construct the result string by flipping the **diagonal elements**.

| i | nums[i] | nums[i][i] | flipped |
|---|---|---|---|
|0|111|1|0|
|1|011|1|0|
|2|001|1|0|

Result string: 000
This string differs from:
111 → different at index 0
011 → different at index 1
001 → different at index 2

So `"000"` **cannot be present in nums**.

---

# 🚀 Algorithm

1. Let `n = nums.size()`
2. Create an empty string `result`
3. Iterate from `0 → n-1`
4. Take the character `nums[i][i]`
5. Flip the bit:
   - `'0' → '1'`
   - `'1' → '0'`
6. Append it to the result
7. Return the result

---

# 💻 C++ Implementation

```cpp
class Solution {
public:
    string findDifferentBinaryString(vector<string>& nums) {

        int n = nums.size();
        string result;

        for(int i = 0; i < n; i++){
            char ch = nums[i][i];

            result += (ch == '0') ? '1' : '0';
        }

        return result;
    }
};
```
## ⏱ Complexity Analysis
### Time Complexity
O(n)

We traverse the list once.

### Space Complexity
O(n)

We create a new binary string of length n.
