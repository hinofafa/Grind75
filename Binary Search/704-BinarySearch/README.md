# Binary Search
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1. <br><br>
You must write an algorithm with $O(log n)$ runtime complexity

Example 1:
> Input: nums = [-1,0,3,5,9,12], target = 9\
Output: 4\
Explanation: 9 exists in nums and its index is 4

Example 2:
> Input: nums = [-1,0,3,5,9,12], target = 2\
Output: -1\
Explanation: 2 does not exist in nums so return -1
 

Constraints:
- $1$ <= nums.length <= $10^4$
- $-10^4$ < nums[i], target < $10^4$
- All the integers in nums are unique.
- nums is sorted in ascending order.

## Solution
Problem can be found in [here](https://leetcode.com/problems/binary-search)!

### [Solution](/Binary%20Search/704-BinarySearch/solution.py)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)-1

        while left <= right:
            mid = (left+right) // 2
            if nums[mid] == target:
                return mid
            # target is in the righthand side of mid, so we need to update left
            elif nums[mid] < target:
                left = mid + 1
            # target is in the lefthand side of mid, so we need to update right
            else:
                right = mid - 1

        return -1
```

Time Complexity: $O(logn)$, Space Complexity: $O(1)$
