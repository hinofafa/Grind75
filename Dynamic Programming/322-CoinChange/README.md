# Coin Change
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money. <br><br>
Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1. <br><br>
You may assume that you have an infinite number of each kind of coin.


Example 1:

> Input: coins = [1,2,5], amount = 11\
Output: 3\
Explanation: 11 = 5 + 5 + 1

Example 2:

> Input: coins = [2], amount = 3\
Output: -1

Example 3:

Input: coins = [1], amount = 0\
Output: 0
 

Constraints:
- 1 <= coins.length <= 12
- 1 <= coins[i] <= $2^{31}$ - 1
- 0 <= amount <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/coin-change)!

### [Solution](/Dynamic%20Programming/322-CoinChange/solution.py): Dynamic Programming

```python
def coinChange(coins: List[int], amount: int) -> int:
    coins_need = [float("inf") for _ in range(amount+1)]
    coins_need[0] = 0
    for i in range(1, amount+1):
        for coin in coins:
            if coin <= i:
                coins_need[i] = min(coins_need[i], coins_need[i-coin]+1)

    return coins_need[-1] if coins_need[-1] != float("inf") else -1
```

Time Complexity: $O(n*m)$, Space Complexity: $O(n)$, where n is value of $amount$ and m is the length of coins.
