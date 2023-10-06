# Contains Duplicate
### <span style="color:green">Easy</span> 

Problem can be found in [here](https://leetcode.com/problems/contains-duplicate)!

> Given an integer array **nums**, return **true** if any value appears at least twice in the array, and return **false** if every element is distinct.

Example 1:
> Input: nums = [1,2,3,1]\
Output: true

Example 2:
> Input: nums = [1,2,3,4]\
Output: false

Example 3:
> Input: nums = [1,1,1,3,3,4,3,2,4,2]\
Output: true

Constraints:
- $1$ <= nums.length <= $10^5$
- $-10^9$ <= nums[i] <= $10^9$

## Solution
### [Basic Solution](/Array/217-ContainsDuplicate/basicSolution.py): Brute Force

```python
def containsDuplicate(nums: List[int]) -> bool:
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] == nums[j]:
                return True

    return False
```

Time Complexity: $O(n^2)$, Space Complexity: O(1)
### [Improved Solution](/Array/217-ContainsDuplicate/improvedSolution.py): Sort

```python
def containsDuplicate(nums: List[int]) -> bool:
    nums.sort()
    left, right = 0, 1
    while right < len(nums):
        if nums[left] == nums[right]:
            return True
        else:
            left, right = right, right + 1

    return False
```

Time Complexity: $O(nlogn)$, Space Complexity: $O(1)$

### [Optimized Solution](/Array/217-ContainsDuplicate/optimizedSolution.py): Set or Hash Table

```python
def containsDuplicate(nums: List[int]) -> bool:
    memo = set()
    for number in nums:
        if number in memo:
            return True
        else:
            memo.add(number)

    return False
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$
