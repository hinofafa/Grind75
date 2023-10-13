# 01 Matrix
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.<br><br>
The distance between two adjacent cells is 1.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)

> Input: mat = [[0,0,0],[0,1,0],[0,0,0]]\
Output: [[0,0,0],[0,1,0],[0,0,0]]

Example 2:

![alt image](https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg)

> Input: mat = [[0,0,0],[0,1,0],[1,1,1]]\
Output: [[0,0,0],[0,1,0],[1,2,1]]
 

Constraints:
- m == mat.length
- n == mat[i].length
- $1$ <= m, n <= $10^4$
- $1$ <= m * n <= $10^4$
- mat[i][j] is either 0 or 1.
- There is at least one 0 in mat.

Problem can be found in [here](https://leetcode.com/problems/01-matrix)!

## Solution
### [Solution](/Graph/542-01Matrix/solution.py): Dynamic Programming

```python
def updateMatrix(matrix: List[List[int]]) -> List[List[int]]:
    distance = [[float("inf") for _ in range(len(matrix[0]))] for _ in range(len(matrix))]

    for row in range(len(matrix)):
        for column in range(len(matrix[0])):
            if matrix[row][column] == 0:
                distance[row][column] = 0
            else:
                if row > 0:
                    distance[row][column] = min(distance[row][column], distance[row-1][column] + 1)
                if column > 0:
                    distance[row][column] = min(distance[row][column], distance[row][column-1] + 1)

    for row in range(len(matrix)-1, -1, -1):
        for column in range(len(matrix[0])-1, -1, -1):
            if row < len(matrix)-1:
                distance[row][column] = min(distance[row][column], distance[row+1][column] + 1)
            if column < len(matrix[0])-1:
                distance[row][column] = min(distance[row][column], distance[row][column+1] + 1)

    return distance
```

Explanation: Observe that for each 1-cell (the value of cell is one), its minimum distance to 0-cell (the value of cell is zero) must come from its four neighbors. We can perform a two-pass algorithm to solve this problem. In this problem, I decide to iterate the matrix from top->bottom & left->right and bottom->top & right->left. One may wonder whether the direction matters. The answer is "No" since if we iterate iterate the matrix from top->bottom & left->right, we are simply finding the shortest among all paths to the top/left/top-left of a given node.
As long as you search in all directions, your answer will be correct.

Time Complexity: $O(mn)$, Space Complexity: $O(1)$, where m is the number of row and n is the number of column.
