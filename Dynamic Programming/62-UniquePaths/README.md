# Unique Paths
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.<br><br>
Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.<br><br>
The test cases are generated so that the answer will be less than or equal to $2 * 10^9$.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

> Input: m = 3, n = 7\
Output: 28

Example 2:

> Input: m = 3, n = 2\
Output: 3\
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
 

Constraints:
- 1 <= m, n <= 100

Problem can be found in [here](https://leetcode.com/problems/unique-paths)!

### [Solution 1](/Dynamic%20Programming/62-UniquePaths/solution1.py): Math

```python
def uniquePaths(m: int, n: int) -> int:
    return comb(m+n-2, n-1)
```

Explanation: There are m+n-2 steps to move from top-left to bottom-right. In m+n-2 steps, there are m-1 steps we have to move down and n-1 steps we have to move right. Simply put, we need to calculate how many ways we could choose m-1 down moves from m+n-2 moves, or n-1 right moves from m+n-2 moves. Therefore, the solution is ![C_{n-1}^{m+n-2}](https://latex.codecogs.com/svg.image?C_{n-1}^{m+n-2}).

Time Complexity: ![O(m+n)](<https://latex.codecogs.com/svg.image?\inline&space;O(m+n)>), Space Complexity: ![O(1)](<https://latex.codecogs.com/svg.image?\inline&space;O(1)>), where m is the number of rows and n is the number of columns.

### [Solution 2](/Dynamic%20Programming/62-UniquePaths/solution2.py): Dynamic Programming

```python
def uniquePaths(m: int, n: int) -> int:
    memo = [1] * n
    for _ in range(1, m):
        for j in range(1, n):
            memo[j] = memo[j - 1] + memo[j]
    return memo[-1] if m and n else 0
```

Time Complexity: $O(m+n)$, Space Complexity: $O(n)$, where m is the number of rows and n is the number of columns.
