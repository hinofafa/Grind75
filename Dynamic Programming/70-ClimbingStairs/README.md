# Climbing Stairs
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> You are climbing a staircase. It takes n steps to reach the top. <br><br>
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


Example 1:

> Input: n = 2\
Output: 2\
Explanation: There are two ways to climb to the top.\
1. 1 step + 1 step\
2. 2 steps

Example 2:

> Input: n = 3\
Output: 3\
Explanation: There are three ways to climb to the top.\
1. 1 step + 1 step + 1 step\
2. 1 step + 2 steps\
3. 2 steps + 1 step

Constraints:
- 1 <= n <= 45

Problem can be found in [here](https://leetcode.com/problems/climbing-stairs)!

### [Solution](/Dynamic%20Programming/70-ClimbingStairs/solution.py): Dynamic Programming

```python
def memoization(func):
    memo = {}

    def helper(self, x):
        if x not in memo:
            memo[x] = func(self, x)
        return memo[x]
    return helper


class Solution:
    @memoization
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        elif n == 2:
            return 2
        else:
            return self.climbStairs(n-1) + self.climbStairs(n-2)
```

Explanation: Basically, it is a Fibonacci sequence. I just use memoization to optimize time complexity.

Time Complexity: $O(n)$, Space Complexity: $O(n)$, where n is value of $n$ steps to climb.
