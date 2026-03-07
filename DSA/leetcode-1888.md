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

# ⚡ Approach 2: Optimized Sliding Window (Without Extra Pattern Strings)

## 💡 Idea

In the first approach, we created two additional strings representing alternating patterns:
101010...
010101...


However, creating these pattern strings requires **extra memory O(n)**.

In this optimized approach, we **avoid storing pattern strings** and instead compute the **expected character dynamically** based on the index.

This reduces the **space complexity from O(n) → O(1)**.

---

# 🔑 Key Observations

An alternating binary string can have only two valid patterns:
Pattern 1 → 1010101010...
Pattern 2 → 0101010101...
These patterns follow a simple rule based on the **index parity**.

### Pattern 1
index even → '1'
index odd → '0'


### Pattern 2
index even → '0'
index odd → '1'


We use this property to **calculate the expected character on the fly**.

---

# 🔄 Handling Rotations Efficiently

The problem allows **rotating the string**.

Example:
Original String
111000

Possible Rotations
111000
110001
100011
000111
001110
011100

Instead of generating all rotations explicitly, we simulate rotations by **traversing indices from `0 → 2n`**.

To access the correct character in the original string, we use:
s[index % n]

This trick allows us to **simulate a doubled string without actually creating one**.

---

# 🪟 Sliding Window Technique

We maintain a **sliding window of size `n`**.

Each window represents **one possible rotation of the string**.

For every window we calculate:
f1 → flips required to match Pattern 1
f2 → flips required to match Pattern 2


The minimum value among these is the answer.

---

# ⚙️ Algorithm

1. Let `n` be the length of the string.
2. Initialize two flip counters:
f1 → flips for pattern 1
f2 → flips for pattern 2
3. Use two pointers:
i → window start
j → window end
4. Traverse indices from `0 → 2n`.
5. For each index:
- Compute expected characters for both patterns.
- Compare them with `s[j % n]`.
6. Increase mismatch counters accordingly.
7. Maintain a **window size of `n`** by removing contributions from the left side.
8. Update the minimum flips whenever window size equals `n`.

---

# 💻 Implementation

```cpp
class Solution {
public:
 int minFlips(string s) {

     int n = s.size();

     int result = INT_MAX;

     int f1 = 0; // flips needed for pattern 1
     int f2 = 0; // flips needed for pattern 2

     int i = 0;
     int j = 0;

     while(j < 2*n){

         char expectedS1 = (j % 2) ? '0' : '1';
         char expectedS2 = (j % 2) ? '1' : '0';

         if(s[j % n] != expectedS1)
             f1++;

         if(s[j % n] != expectedS2)
             f2++;

         if(j - i + 1 > n){

             char expectedS1 = (i % 2) ? '0' : '1';
             char expectedS2 = (i % 2) ? '1' : '0';

             if(s[i % n] != expectedS1)
                 f1--;

             if(s[i % n] != expectedS2)
                 f2--;

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
## ⏱️ Complexity Analysis
### Time Complexity
O(n)

We iterate through 2n positions using a sliding window.

Each element is processed at most twice.

### Space Complexity
O(1)

No additional pattern strings are stored.

Only a few integer variables are used.
