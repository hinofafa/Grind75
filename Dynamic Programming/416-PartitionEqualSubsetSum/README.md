# Partition Equal Subset Sum
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.


Example 1:

> Input: nums = [1,5,11,5]\
Output: true\
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Example 2:

> Input: nums = [1,2,3,5]\
Output: false\
Explanation: The array cannot be partitioned into equal sum subsets.
 

Constraints:
- 1 <= nums.length <= 200
- 1 <= nums[i] <= 100

Problem can be found in [here](https://leetcode.com/problems/partition-equal-subset-sum)!

### [Solution 1](/Dynamic%20Programming/416-PartitionEqualSubsetSum/solution1.py): Dynamic Programming + Tabulation

```python
def canPartition(nums: List[int]) -> bool:
    total_sum = sum(nums)
    if total_sum % 2 == 1:
        return False

    half_sum = total_sum // 2
    memo = [True] + [False]*half_sum
    for num in nums:
        for j in range(half_sum, num-1, -1):
            memo[j] |= memo[j-num]

    return memo[half_sum]
```

Time Complexity: $O(nm)$, Space Complexity: $O(m)$, where n is the length of array and m is the sum of array.

### [Solution 2](/Dynamic%20Programming/416-PartitionEqualSubsetSum/solution2.py): Dynamic Programming + Bitwise Operations

```python
def canPartition(nums: List[int]) -> bool:
    total_sum = sum(nums)
    if total_sum % 2 == 0:
        return False

    half_sum, bit = total_sum // 2, 1
    for num in nums:
        bit |= bit << num

    return bit & 1 << half_sum
```

Time Complexity: $O(nm)$, Space Complexity: $O(m)$, where n is the length of array and m is the sum of array.
