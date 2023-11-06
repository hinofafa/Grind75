# Ransom Note
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise. <br><br>
Each letter in magazine can only be used once in ransomNote.
 

Example 1:
> Input: ransomNote = "a", magazine = "b"\
Output: false

Example 2:
> Input: ransomNote = "aa", magazine = "ab"\
Output: false

Example 3:
> Input: ransomNote = "aa", magazine = "aab"\
Output: true

Constraints:
- $1$ <= ransomNote.length, magazine.length <= $10^5$
- ransomNote and magazine consist of lowercase English letters.

Problem can be found in [here](https://leetcode.com/problems/ransom-note)!

### [Solution](/Hash%20Table/383-RansomNote/solution.py): Hash Table

```python
def canConstruct(ransomNote: str, magazine: str) -> bool:
    memo = defaultdict(int)
    for char in magazine:
        memo[char] += 1

    for char in ransomNote:
        if memo[char] == 0:
            return False

        memo[char] -= 1

    return True
```

Time Complexity: $O(n+m)$, Space Complexity: $O(1)$, where n is the length of ransomNote and m is the length of magazine.
