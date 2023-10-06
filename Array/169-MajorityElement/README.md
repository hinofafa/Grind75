# Majority Element
### <span style="color:green">Easy</span> 

Problem can be found in [here](https://leetcode.com/problems/majority-element/)!

> Given an array **nums** of size **n**, return the majority element. <br><br>
The majority element is the element that appears more than **⌊n / 2⌋** times. You may assume that the majority element always exists in the array.


Example 1:
> Input: nums = [3,2,3]\
Output: 3

Example 2:
> Input: nums = [2,2,1,1,1,2,2]\
Output: 2
 
Constraints:
- n == nums.length
- $1$ <= n <= $5 * 10^4$
- $-10^9$ <= nums[i] <= $10^9$
 

Follow-up: Could you solve the problem in linear time and in $O(1)$ space?

## Solution
### [Basic Solution](/Array/169-MajorityElement/BasicSolution.py): Brute Force

```python
def majorityElement(nums: List[int]) -> int:
    for i in range(len(nums)):
        counter = sum(1 for number in nums if number == nums[i])
        if counter > len(nums) // 2:
            return nums[i]
```

Time Complexity: $O(n^2)$, Space Complexity: $O(1)$

### [Improved Solution](/Array/169-MajorityElement/ImprovedSolution.py): Hash Table

```python
def majorityElement(nums: List[int]) -> int:
    memo = {}
    threshold = len(nums) // 2
    for number in nums:
        try:
            memo[number] += 1
        except KeyError:
            memo[number] = 1

        if memo[number] > threshold:
                return number
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$
