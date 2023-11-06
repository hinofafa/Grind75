# Word Search
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an m x n grid of characters board and a string word, return true if word exists in the grid. <br><br>
The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.


Example 1:

![alt image](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

> Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"\
Output: true

Example 2:

![alt image](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

> Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"\
Output: true

Example 3:

![alt image](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

> Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"\
Output: false

Constraints:
- m == board.length
- n = board[i].length
- $1$ <= m, n <= $6$
- $1$ <= word.length <= $15$
- board and word consists of only lowercase and uppercase English letters.
 
Follow up: Could you use search pruning to make your solution faster with a larger board?

Problem can be found in [here](https://leetcode.com/problems/word-search)!

## Solution
### [Solution](/Graph/79-WordSearch/solution.py): Depth-First Search

```python
def exist(board: List[List[str]], word: str) -> bool:
    def DFS(row: int, column: int, word_index: int) -> None:
        nonlocal is_word_exist
        # To avoid further function calls as we have already found the answer
        if is_word_exist:
            return
        # This means that we have found the answer
        if word_index == len(word):
            is_word_exist = True
            return
        # Check if we exceed boundaries
        if row == -1 or row == row_number or column == -1 or column == column_number:
            return

        # Store its value for restoring purpose
        data = board[row][column]
        # Update its value to empty char to avoid using same cell twice
        board[row][column] = ""
        if data == word[word_index]:
            DFS(row+1, column, word_index+1)
            DFS(row-1, column, word_index+1)
            DFS(row, column+1, word_index+1)
            DFS(row, column-1, word_index+1)
        # If no solution is found, then updated to its initial value
        board[row][column] = data

    is_word_exist = False
    row_number, column_number = len(board), len(board[0])
    for row in range(row_number):
        for column in range(column_number):
            if board[row][column] == word[0]:
                DFS(row, column, 0)
            if is_word_exist:
                break

    return is_word_exist
```

Time Complexity: $O(m*n*3^w)$, Space Complexity: $O(m*n)$, where m is the number of row, n is the number of column, and w is the length of word.
