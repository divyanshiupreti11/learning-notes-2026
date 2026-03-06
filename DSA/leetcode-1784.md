# LeetCode 1784 - Check if Binary String Has at Most One Segment of Ones

## 🔗 Problem Link
https://leetcode.com/problems/check-if-binary-string-has-at-most-one-segment-of-ones/description/?envType=daily-question&envId=2026-03-06

## 🧠 Problem Statement
Given a binary string `s` containing only `0`s and `1`s, return **true** if the string contains **at most one contiguous segment of ones**. Otherwise, return **false**.

A segment of ones means a continuous group of `1`s.

---

## 📌 Examples

### Example 1
Input:s = "1001"

Segments of `1`:  [1]00[1]

There are **2 segments of ones**, so the answer is: false 

### Example 2
Input: s = "110"

Segments of `1`: [11]0

There is **only one segment of ones**, so the answer is: true

## 💡  Approach

We count how many **segments of `1`** exist in the string.

A **new segment starts** when:
current character = '1'
previous character = '0'

This indicates that a new group of `1`s has started.

### 🚀 Steps

1. Initialize `cnt = 0` to count segments.
2. If the first character is `1`, increment `cnt`.
3. Traverse the string from index `1`.
4. If `s[i] == '1'` and `s[i-1] == '0'`, increment `cnt`.
5. Finally check: cnt <= 1

Because the problem says **"at most one segment"**.

So valid cases are:
0 segment
1 segment


Invalid cases:
2 or more segments



