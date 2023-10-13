# Number of Islands
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands. <br><br>
An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
> Input: grid = [ \
  ["1","1","1","1","0"],\
  ["1","1","0","1","0"],\
  ["1","1","0","0","0"],\
  ["0","0","0","0","0"]\
]\
Output: 1

Example 2:
> Input: grid = [\
  ["1","1","0","0","0"],\
  ["1","1","0","0","0"],\
  ["0","0","1","0","0"],\
  ["0","0","0","1","1"]\
]\
Output: 3

Constraints:
- m == grid.length
- n == grid[i].length
- $1$ <= m, n <= $300$
- grid[i][j] is '0' or '1'.

Problem can be found in [here](https://leetcode.com/problems/number-of-islands)!

## Solution
### [Solution](/Graph/200-NumberofIslands/solution.py): Depth-First Search

```python
def numIslands(grid: List[List[str]]) -> int:
    def dfs(row: int, column: int) -> None:
        exceed_boundaries = row < 0 or column < 0 or row >= number_of_row or column >= number_of_column
        if exceed_boundaries or grid[row][column] == "0":
            return

        grid[row][column] = "0"
        dfs(row-1, column)
        dfs(row+1, column)
        dfs(row, column-1)
        dfs(row, column+1)

    number_of_islands = 0
    number_of_row, number_of_column = len(grid), len(grid[0])
    for i in range(number_of_row):
        for j in range(number_of_column):
            if grid[i][j] == "1":
                dfs(i, j)
                number_of_islands += 1

    return number_of_islands
```

Explanation: Everytime we find a land ("1"), we perform DFS (depth-first search) to find all of the land in this island and change it to water ("0") so that we will not count it again in further iterations. After DFS, we have fully explored this particular island. Notice that it is feasible to change it to another character whatever you like except "1".

Time Complexity: $O(nm)$, Space Complexity: $O(nm)$, where n is the number of row and m is the number of column.
