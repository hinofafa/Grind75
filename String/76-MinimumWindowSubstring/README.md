# Minimum Window Substring
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard` 

> Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "". <br><br>
The testcases will be generated such that the answer is unique.

 

Example 1:
> Input: s = "ADOBECODEBANC", t = "ABC"\
Output: "BANC"\
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:
> Input: s = "a", t = "a"\
Output: "a"\
Explanation: The entire string s is the minimum window.

Example 3:
> Input: s = "a", t = "aa"\
Output: ""\
Explanation: Both 'a's from t must be included in the window.\
Since the largest window of s only has one 'a', return empty string.
 

Constraints:
- m == s.length
- n == t.length
- $1$ <= m, n <= $10^5$
- s and t consist of uppercase and lowercase English letters.
 

Follow up: Could you find an algorithm that runs in $O(m + n)$ time?

Problem can be found in [here](https://leetcode.com/problems/minimum-window-substring)!

## Solution
### [Solution](/String/76-MinimumWindowSubstring/solution.py)

```python
def minWindow(s: str, t: str) -> str:
    missing_counter = len(t)
    window_start = window_end = current = 0
    memo = collections.Counter(t)

    for index, token in enumerate(s, 1):
        # Expand to find a valid window
        if memo[token] > 0:
            missing_counter -= 1
        memo[token] -= 1

        # Find a valid window
        if missing_counter == 0:
            # Contract to find a smaller and valid window
            while current < index and memo[s[current]] < 0:
                memo[s[current]] += 1
                current += 1

            if window_end == 0 or index-current < window_end-window_start:
                window_start, window_end = current, index

            # Move forward to find a new window
            memo[s[current]] += 1
            missing_counter += 1
            current += 1

    return s[window_start:window_end]
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$