# Word Break
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.<br><br>
Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:
> Input: s = "leetcode", wordDict = ["leet","code"]\
Output: true\
Explanation: Return true because "leetcode" can be segmented as "leet code".

Example 2:
> Input: s = "applepenapple", wordDict = ["apple","pen"]\
Output: true\
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".\
Note that you are allowed to reuse a dictionary word.

Example 3:
> Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]\
Output: false

Constraints:
- 1 <= s.length <= 300
- 1 <= wordDict.length <= 1000
- 1 <= wordDict[i].length <= 20
- s and wordDict[i] consist of only lowercase English letters.
- All the strings of wordDict are unique.

Problem can be found in [here](https://leetcode.com/problems/word-break)!

### [Solution](/Trie/139-WordBreak/solution.py): Dynamic Programming

```python
def wordBreak(s: str, wordDict: List[str]) -> bool:
    words = set(wordDict)
    has_combination = [True] + [False] * len(s)
    max_word_length = max(len(word) for word in words)
    for i in range(1, len(s)+1):
        for j in range(max(0, i-max_word_length), i):
            if not has_combination[i]:
                has_combination[i] = has_combination[j] and s[j:i] in words

    return has_combination[-1]
```

Time Complexity: $O(n^3)$, Space Complexity: $O(n)$, where n is the length of $s$.
