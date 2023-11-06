# Word Ladder
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard` 

> A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> $s_1$ -> $s_2$ -> ... -> $s_k$ such that:
- Every adjacent pair of words differs by a single letter.
- Every $s_i$ for $1$ <= $i$ <= $k$ is in wordList. Note that beginWord does not need to be in wordList.
- $s_k$ == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.
 

Example 1:

> Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]\
Output: 5\
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

Example 2:

> Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]\
Output: 0\
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
 

Constraints:
- 1 <= beginWord.length <= 10
- endWord.length == beginWord.length
- 1 <= wordList.length <= 5000
- wordList[i].length == beginWord.length
- beginWord, endWord, and wordList[i] consist of lowercase English letters.
- beginWord != endWord
- All the words in wordList are unique.

Problem can be found in [here](https://leetcode.com/problems/word-ladder)!

### [Solution](/Graph/127-WordLadder/solution.py): Breadth-First Search

```python
def ladderLength(beginWord: str, endWord: str, wordList: List[str]) -> int:
    memo = set(wordList)
    queue = deque([(beginWord, 0)])

    while queue:
        word, counter = queue.popleft()
        if word == endWord:
            return counter+1
        for i in range(len(word)):
            for char in ascii_lowercase:
                new_word = word[:i] + char + word[i+1:]
                if new_word in memo:
                    memo.remove(new_word)
                    queue.append((new_word, counter+1))

    return 0
```

Time Complexity: $O(N*M^2)$, Space Complexity: $O(N)$, where N is the length of wordList and M is the length of word.
