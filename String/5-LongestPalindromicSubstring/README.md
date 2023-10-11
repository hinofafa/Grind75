# Longest Palindromic Substring
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a string s, return the longest palindromic substring in s.

Example 1:
> Input: s = "babad"\
Output: "bab"\
Explanation: "aba" is also a valid answer.

Example 2:
> Input: s = "cbbd"\
Output: "bb"

Constraints:
- $1$ <= s.length <= $1000$
- s consist of only digits and English letters.

Problem can be found in [here](https://leetcode.com/problems/longest-palindromic-substring)!

## Solution
### [Solution](/String/5-LongestPalindromicSubstring/solution.py): Dynamic Programming

```python
def longestPalindrome(s: str) -> str:
    longest_palindrome = s[0]
    memo = [[False] * len(s) for _ in range(len(s))]

    for i in range(len(s)):
        memo[i][i] = True

    for i in range(len(s)):
        for j in range(i-1, -1, -1):
            if s[i] == s[j]:
                if i == j+1 or memo[i-1][j+1]:
                    memo[i][j] = True
                    if i-j+1 > len(longest_palindrome):
                        longest_palindrome = s[j:i+1]

    return longest_palindrome
```

Time Complexity: $O(n^2)$, Space Complexity: $O(n^2)$