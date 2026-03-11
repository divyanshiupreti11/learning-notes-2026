# 🔢 Bitwise Complement of an Integer
## :link: Problem Link
https://leetcode.com/problems/complement-of-base-10-integer/?envType=daily-question&envId=2026-03-11

## 📌 Problem
Given a non-negative integer `n`, return the **bitwise complement** of its binary representation.

The **bitwise complement** flips every bit:
- `0 → 1`
- `1 → 0`

### Example

| Decimal | Binary | Complement | Result |
|--------|--------|-----------|--------|
| 5 | 101 | 010 | 2 |
| 10 | 1010 | 0101 | 5 |

---

# 💡 Approach

To compute the complement, we create a **mask** containing all `1`s for the number of bits in `n`.

Example:


n = 5
Binary = 101

Mask = 111

101 XOR 111 = 010


Steps:
1. Handle the edge case when `n = 0`.
2. Create a mask containing all `1`s with the same number of bits as `n`.
3. XOR the mask with `n` to flip the bits.

---

# ⚙️ Algorithm

1️⃣ If `n == 0`, return `1`.

2️⃣ Copy `n` into a temporary variable `temp`.

3️⃣ Construct the mask using:


mask = (mask << 1) | 1


4️⃣ Continue until all bits of `temp` are processed.

5️⃣ Return the complement using XOR.

---

# 💻 C++ Implementation

```cpp
class Solution {
public:
    int bitwiseComplement(int n) {
        if(n==0) return 1;

        int mask = 0;
        int temp = n;

        while(temp > 0){
            mask = (mask << 1) | 1;
            temp = temp >> 1;
        }

        return n ^ mask;
    }
};
```
## ⏱️ Complexity Analysis

### Time Complexity: **O(log n)**

**Reason:** The loop runs once for each bit of `n`, and the number of bits in an integer `n` is **log₂(n)**.

---

### Space Complexity: **O(1)**

**Reason:** Only constant extra variables (`mask`, `temp`) are used regardless of input size.
