# 🧩 LeetCode 1415 - The k-th Lexicographical Happy String of Length n
# 🔗 Problem Link
https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/?envType=daily-question&envId=2026-03-14

## 📌 Problem Overview
A **happy string** is defined as a string that:
- Contains only characters `'a'`, `'b'`, `'c'`
- Does **not** contain two identical consecutive characters

The task is to return the **k-th lexicographical happy string** of length `n`.

If there are fewer than `k` happy strings, return an **empty string**.

---

## 💡 Approach (Backtracking)

We generate all possible **happy strings** using **Backtracking (Recursion)**.

### ⚙️ Steps
1. Start with an empty string `curr`.
2. Try adding characters `'a'`, `'b'`, `'c'`.
3. If the last character of `curr` is the same as the current character, **skip it**.
4. Otherwise:
   - Add the character
   - Call recursion
   - Backtrack using `pop_back()`
5. When `curr.length() == n`, store the string in `result`.
6. After generating all strings, return the **k-th string (1-indexed)**.
7. If `k` is greater than the number of happy strings, return `""`.

---

## 🧑‍💻 C++ Code

```cpp
class Solution {
public:
   void solve(int& n,string& curr,vector<string>& result){
        if(curr.length()==n){
            result.push_back(curr);
            return;
        }

        for(char ch='a';ch<='c';ch++){
            if(!curr.empty() && curr.back()==ch) continue;

            curr.push_back(ch);
            solve(n,curr,result);
            curr.pop_back();
        }
   }

    string getHappyString(int n, int k) {
        string curr="";
        vector<string> result;

        solve(n,curr,result);

        if(k>result.size()) return "";

        return result[k-1];
    }
};
```

---

## ⏱️ Time Complexity
```
O(2^n)
```

Explanation:
- First character → **3 choices**
- Remaining characters → **2 choices each**

Total possible strings ≈ **3 × 2^(n−1)**

---

## 💾 Space Complexity
```
O(2^n)
```

Used for:
- Storing happy strings in the `result` vector
- Recursion stack space

---
