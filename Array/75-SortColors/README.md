# Sort Colors
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue. <br><br>
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.<br><br>
You must solve this problem without using the library's sort function.

Example 1:
> Input: nums = [2,0,2,1,1,0]\
Output: [0,0,1,1,2,2]

Example 2:
> Input: nums = [2,0,1]\
Output: [0,1,2]
 

Constraints:
- n == nums.length
- $1$ <= n <= $300$
- nums[i] is either $0$, $1$, or $2$.
 

Follow up: Could you come up with a one-pass algorithm using only constant extra space?

Problem can be found in [here](https://leetcode.com/problems/sort-colors)!

## Solution
### [Solution](/Array/75-SortColors/solution.py): Three Pointers

```python
# 0: red, 1: white, 2: blue
def sortColors(nums: List[int]) -> None:
    left, mid, right = 0, 0, len(nums)-1
    while mid <= right:
        if nums[mid] == 0:
            nums[left], nums[mid] = nums[mid], nums[left]
            left += 1
            mid += 1
        elif nums[mid] == 2:
            nums[right], nums[mid] = nums[mid], nums[right]
            right -= 1
        else:
            mid += 1
```

Explanation: Use three pointers to perform in-place sorting. If nums[mid] is 0, meaning that we need to swap the value in nums[left] and nums[mid] to make the array sorted. Another case is that if we encounter 2 in nums[mid], we know that we should swap nusmms[right] and nums[mid] to keep the array sorted. By doing so, the array will be sorted in O(n) time after iterating the whole array (worst case).

Time Complexity: $O(n)$, Space Complexity: $O(1)$