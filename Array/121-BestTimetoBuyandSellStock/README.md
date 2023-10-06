# Best Time to Buy and Sell Stock
### <span style="color:green">Easy</span> 

Problem can be found in [here](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)!

> You are given an array **prices** where **prices[i]** is the price of a given stock on the **$i^{th}$** day. <br><br>
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. <br><br>
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return **0**.

Example 1:

> Input: prices = [7,1,5,3,6,4]\
Output: 5\
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.\
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:

> Input: prices = [7,6,4,3,1]\
Output: 0\
Explanation: In this case, no transactions are done and the max profit = 0.

Constraints:
- $1$ <= prices.length <= $10^5$
- $0$ <= prices[i] <= $10^4$

## Solution

### [Solution 1](/Array/121-BestTimetoBuyandSellStock/solution1.py): Left Right Pointer

```python
 def maxProfit(prices: List[int]) -> int:
    maxGap = 0
    left, right = 0, 1
    while right < len(prices):
        if prices[left] < prices[right]:
            maxGap = max(maxGap, prices[right] - prices[left])
            right += 1
        else:
            left, right = right, right + 1

    return maxGap
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$

Explanation: We cannot buy a stock in the future and sell it now in stock market; thus, we only need to store the lowest stock price in every iteration. And in next iteration, we only need to check whether current stock price is higher than previous lowest stock price. If so, then we might need to update _maxGap_. On the other hand, if current stock price is lower than previous lowest price, then we need to update two pointers (_left_, _right_).

### [Solution 2](/Array/121-BestTimetoBuyandSellStock/solution2.py): Min Max

```python
def maxProfit(prices: List[int]) -> int:
    buyPrice, maxGap = float("inf"), 0
    for price in prices:
        buyPrice, maxGap = min(buyPrice, price), max(maxGap, price - buyPrice)

    return maxGap
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$

Explanation: Instead of using two variables to store the index of the lowest and current price of stock like [solution 1](#solution-1array121-besttimetobuyandsellstocksolution1py-left-right-pointer), we only need to store the lowest price as iteration goes on. If we find current price is less than pervious lowest price, then it is possible that the maximum profit might change. Therefore, we might need to update the value of _maxGap_ as shown in the code section above.
