# Two Sum 
### <span style="color:green">Easy</span> 

Problem can be found in [here](https://leetcode.com/problems/two-sum/)!

> Given an array of integers **nums** and an integer **target**, return indices of the two numbers such that they add up to **target**. <br><br>
You may assume that each input would have exactly one solution, and you may not use the same element twice. <br><br>
You can return the answer in any order.

Example 1:
> Input: nums = [2,7,11,15], target = 9 \
Output: [0,1] \
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
> Input: nums = [3,2,4], target = 6\
Output: [1,2]

Example 3:
> Input: nums = [3,3], target = 6\
Output: [0,1]

Constraints:
- $2$ <= nums.length <= $10^4$
- $-10^9$ <= nums[i] <= $10^9$
- $-10^9$ <= target <= $10^9$
- Only one valid answer exists.

Follow-up: Can you come up with an algorithm that is less than **$O(n^2)$** time complexity?

## Solution

### [Basic Solution](/Array/1-TwoSum/basicSolution.py): Brute Force

```python
# target: int, nums: List[int]

 for i in range(len(nums)):
    number_to_find = target - nums[i]
    for j in range(i + 1, len(nums)):
        if nums[j] == number_to_find:
            return [i, j] # Find indices of the two numbers!
```

Time Complexity: $O(n^2)$, Space Complexity: $O(1)$

Explanation: Simply iterate the array and find the target value among the array in each iteration.

### [Improved Solution](/Array/1-TwoSum/improvedSolution.py): Hash Table

```python
memo = {}
for i, j in enumerate(nums):
    number_to_find = target - j
    try:
        return [memo[j], i] # Find indices of the two numbers!
    except KeyError:
        memo[number_to_find] = i
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$

Explanation: Instead of searching the whole array blindlessly in each iteration, using a hash table can determine whether this element is the target value in $O(1)$ time.
