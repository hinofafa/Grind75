# Rotting Oranges
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

You are given an m x n grid where each cell can have one of three values:
- 0 representing an empty cell,
- 1 representing a fresh orange, or
- 2 representing a rotten orange.

> Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten. <br><br>
Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

> Input: grid = [[2,1,1],[1,1,0],[0,1,1]]\
Output: 4

Example 2:

> Input: grid = [[2,1,1],[0,1,1],[1,0,1]]\
Output: -1\
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

Example 3:

> Input: grid = [[0,2]]\
Output: 0\
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.
 

Constraints:
- m == grid.length
- n == grid[i].length
- $1$ <= m, n <= $10$
- grid[i][j] is $0$, $1$, or $2$.

Problem can be found in [here](https://leetcode.com/problems/rotting-oranges)!

## Solution
### [Solution](/Graph/994-RottingOranges/solution.py): Breadth-First Search

```python
def orangesRotting(grid: List[List[int]]) -> int:
    def BFS(row, column):
        """ Check whether its neighbors are fresh. If so, update and push into queue. """
        if row > 0 and grid[row-1][column] == 1:
            grid[row-1][column] = 2
            fresh_oranges -= 1
            rotten_oranges.append([row-1, column])
        if row < number_of_row-1 and grid[row+1][column] == 1:
            grid[row+1][column] = 2
            fresh_oranges -= 1
            rotten_oranges.append([row+1, column])
        if column > 0 and grid[row][column-1] == 1:
            grid[row][column-1] = 2
            fresh_oranges -= 1
            rotten_oranges.append([row, column-1])
        if column < number_of_column-1 and grid[row][column+1] == 1:
            grid[row][column+1] = 2
            fresh_oranges -= 1
            rotten_oranges.append([row, column+1])

    # Initialization
    rotten_oranges = deque()
    counter = fresh_oranges = 0
    number_of_row, number_of_column = len(grid), len(grid[0])
    for i in range(number_of_row):
        for j in range(number_of_column):
            if grid[i][j] == 1:
                fresh_oranges += 1
            elif grid[i][j] == 2:
                rotten_oranges.append([i, j])

    # Simulate the rotten process
    while rotten_oranges and fresh_oranges:
        for _ in range(len(rotten_oranges)):
            row, column = rotten_oranges.popleft()
            BFS(row, column)
        counter += 1

    return counter if fresh_oranges == 0 else -1
```

Explanation: In the initial stage, we need to iterate the whole grid once to compute the number of fresh oranges and the location of rotten oranges. In each iteration (minute), we perform a one-level BFS (breadth-first search) for all rotten oranges. If we find a fresh orange next to a rotten orange, we update a fresh orange to rotten one and the number of remaining fresh oranges. Once the number of fresh oranges is 0 or there are no rotten oranges in the queue, we know the algorithm is finished.

Time Complexity: $O(mn)$, Space Complexity: $O(m+n)$, where m is the number of row and n is the number of column.
