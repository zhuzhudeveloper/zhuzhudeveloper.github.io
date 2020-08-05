---
category: algorithm
tags: manacher, palindromic substring
---
# Manacher's Algorithm
## Detailed Explanation
https://zhuanlan.zhihu.com/p/70532099

https://www.cxyxiaowu.com/2665.html

https://www.jianshu.com/p/392172762e55
### Examples
#### LeetCode 647: Palindromic Substrings
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:

Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
    def countSubstrings(self, s: str) -> int:
        A = '@#' + '#'.join(s) + '#$'
        P = [0] * len(A)
        center = right = 0
        count = 0
        for i in range(1, len(A)-1):
            if i < right:
                P[i] = min(right-i, P[2 * center - i])
            while A[i + P[i] + 1] == A[i - P[i] - 1]:
                P[i] += 1
            if i + P[i] > right:
                center, right = i, i + P[i]
            print(P[i])
            if A[i] != '#' or P[i] > 1:
                count += (P[i]+1) // 2
        return count
```
