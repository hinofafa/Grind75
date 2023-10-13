# Search in Rotated Sorted Array

> There is an integer array nums sorted in ascending order (with distinct values). <br><br>
Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2]. <br><br>
Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums. <br><br>
You must write an algorithm with $O(log n)$ runtime complexity.

Example 1:
> Input: nums = [4,5,6,7,0,1,2], target = 0\
Output: 4

Example 2:
> Input: nums = [4,5,6,7,0,1,2], target = 3\
Output: -1

Example 3:
> Input: nums = [1], target = 0\
Output: -1

Constraints:
- $1$ <= nums.length <= $5000$
- $-10^4$ <= nums[i] <= $10^4$
- All values of nums are unique.
- nums is an ascending array that is possibly rotated.
- $-10^4$ <= target <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/search-in-rotated-sorted-array)!

## Solution
### [Solution](/Binary%20Search/33-SearchinRotatedSortedArray/solution.py)

```python
def search(nums: List[int], target: int) -> int:
    left, right = 0, len(nums)-1

    while left <= right:
        # avoid the potential overflow porblem in other programming language, but not including Python
        mid = left + (right-left) // 2
        if nums[mid] == target:
            return mid

        # The left-handed side of mid in nums is ordered
        if nums[mid] >= nums[left]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        
        # The right-handed side of mid in nums is ordered
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```

Explanation: The difference between the typical binary search problem in a sorted array and this problem is that the array may be possibly rotated somewhere in the array. To perform binary search in this problem, we need to check whether the target is in the left-rotated side or right-rotated side. For instance, assume that there is an array A = [3, 4, 5, 6, 7, 0, 1, 2] and our target number is 7. In this case, the left-rotated side is [3, 4, 5, 6, 7] while the right-rotated side is [0, 1, 2]. We need to determine whether the middle of left and right pointers is in the right-rotated or left-rotated side. To find out which side we are, we can simply achieve so by comparing the value of A[left] and A[mid]. If we are in the left-rotated side, search A[left] ~ A [mid] if A[left] <= target < A[mid] else, search right side. If we are in the right-rotated side, search in A[mid] ~ A[right] if A[mid] < target <= A[right] else, search left side.

Time Complexity: $O(logn)$, Space Complexity: $O(1)$
