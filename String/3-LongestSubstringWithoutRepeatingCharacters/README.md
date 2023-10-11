## Longest Substring Without Repeating Characters
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a string s, find the length of the longest substring without repeating characters.

Example 1:
> Input: s = "abcabcbb"\
Output: 3\
Explanation: The answer is "abc", with the length of 3.

Example 2:
> Input: s = "bbbbb"\
Output: 1\
Explanation: The answer is "b", with the length of 1.

Example 3:
> Input: s = "pwwkew"\
Output: 3\
Explanation: The answer is "wke", with the length of 3.\
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 
Constraints:
- $0$ <= s.length <= $5 * 10^4$
- s consists of English letters, digits, symbols and spaces.

Problem can be found in [here](https://leetcode.com/problems/longest-substring-without-repeating-characters)!

## Solution
### [Solution1](/String/3-LongestSubstringWithoutRepeatingCharacters/solution1.py): Hash Table

```python
def lengthOfLongestSubstring(s: str) -> int:
    memo = {}
    max_length = pointer = 0

    for index, token in enumerate(s):
        # pointer <= memo[token] checks whether we have skipped that token before
        if token in memo and pointer <= memo[token]:
            pointer = memo[token] + 1
        else:
            max_length = max(max_length, index-pointer+1)
        memo[token] = index

    return max_length
```

Time Complexity: $O(n)$, Space Complexity: $O(m)$, where n is the length of s and m is the length of the longest substring.

### [Solution2](/String/3-LongestSubstringWithoutRepeatingCharacters/solution2.py): Sliding Window

```python
def lengthOfLongestSubstring(s: str) -> int:
    memo = set()
    window_start = window_end = max_length = 0

    while window_start < len(s) and window_end < len(s):
        token = s[window_end]
        if token in memo:
            memo.remove(s[window_start])
            window_start += 1
        else:
            window_end += 1
            max_length = max(max_length, window_end-window_start)
            memo.add(token)

    return max_length
```

Time Complexity: $O(n)$, Space Complexity: $O(m)$, where n is the length of s and m is the length of the longest substring.
