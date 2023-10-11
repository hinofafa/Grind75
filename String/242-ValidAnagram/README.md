# Valid Anagram
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given two strings s and t, return true if t is an anagram of s, and false otherwise.<br><br>
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.
 
Example 1:
> Input: s = "anagram", t = "nagaram"\
Output: true

Example 2:
> Input: s = "rat", t = "car"\
Output: false

Constraints:
- $1$ <= s.length, t.length <= $5 * 10^4$
- s and t consist of lowercase English letters.
 
Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

Problem can be found in [here](https://leetcode.com/problems/valid-anagram)!

## Solution
### [Solution](/String/242-ValidAnagram/solution.py): Hash Table

```python
def isAnagram(s: str, t: str) -> bool:
    memo = {}
    for token in s:
        try:
            memo[token] += 1
        except KeyError:
            memo[token] = 1

    for token in t:
        try:
            memo[token] -= 1
        except KeyError:
            return False

    return all(count == 0 for count in memo.values())
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$
