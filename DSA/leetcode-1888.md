# Minimum Flips to Make Binary String Alternating
## 🔗 problem link
https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/description/?envType=daily-question&envId=2026-03-07

## 🔄 Problem Statement

Given a binary string `s`, return the **minimum number of flips** required to make the string **alternating**.

A binary string is alternating if no two adjacent characters are the same.

Valid alternating strings:
010101...
101010...


Additionally, the string can be **rotated any number of times**.

A rotation moves the first character of the string to the end.

Example rotations of `"111000"`:
111000
110001
100011
000111
001110
011100

We must compute the **minimum number of flips required for any rotation of the string**.

---

## 💡 Key Idea

Instead of explicitly generating all rotations, we use a common trick:
s + s

This allows us to simulate every possible rotation of the string.

Then we apply a **sliding window of size `n`** to evaluate each possible rotation.

For every window, we compare it with two possible alternating patterns:

Pattern 1 → 101010...
Pattern 2 → 010101...

The minimum mismatches with these patterns give the answer.

---

# 🚀 Approach 1: Using Explicit Alternating Strings

## 💡Idea

1. Double the string (`s = s + s`) to simulate rotations.
2. Generate two alternating pattern strings:
   - `s1 = 101010...`
   - `s2 = 010101...`
3. Use a **sliding window of size `n`**.
4. Count mismatches with both patterns.
5. Track the **minimum number of flips**.

---

## 💻 Code

```cpp
class Solution {
public:
    int minFlips(string s) {

        int n = s.size();
        s = s + s;

        string s1, s2;

        for(int i = 0; i < 2*n; i++){
            s1 += (i % 2) ? '0' : '1';
            s2 += (i % 2) ? '1' : '0';
        }

        int result = INT_MAX;
        int f1 = 0, f2 = 0;

        int i = 0, j = 0;

        while(j < 2*n){

            if(s[j] != s1[j]) f1++;
            if(s[j] != s2[j]) f2++;

            if(j - i + 1 > n){

                if(s[i] != s1[i]) f1--;
                if(s[i] != s2[i]) f2--;

                i++;
            }

            if(j - i + 1 == n){
                result = min({result, f1, f2});
            }

            j++;
        }

        return result;
    }
};
```
## ⏰ Complexity Analysis
### Time Complexity
O(n)
The sliding window iterates over 2n characters once.
### Space Complexity
O(n)
Two additional pattern strings are stored.
