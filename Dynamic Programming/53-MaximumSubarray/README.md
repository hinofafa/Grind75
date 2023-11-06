# Maximum Subarray
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Medium`

> Given an integer array nums, find the 
subarray with the largest sum, and return its sum.


Example 1:

> Input: nums = [-2,1,-3,4,-1,2,1,-5,4]\
Output: 6\
Explanation: The subarray [4,-1,2,1] has the largest sum 6.

Example 2:

> Input: nums = [1]\
Output: 1\
Explanation: The subarray [1] has the largest sum 1.

Example 3:

> Input: nums = [5,4,-1,7,8]\
Output: 23\
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
 

Constraints:
- $1$ <= nums.length <= $10^5$
- $-10^4$ <= nums[i] <= $10^4$
 

Follow up: If you have figured out the $O(n)$ solution, try coding another solution using the divide and conquer approach, which is more subtle.

Problem can be found in [here](https://leetcode.com/problems/maximum-subarray)!

### [Solution](/Dynamic%20Programming/53-MaximumSubarray/solution.py): Dynamic Programming

```python
def maxSubArray(nums: List[int]) -> int:
    for i in range(1, len(nums)):
        nums[i] = max(nums[i], nums[i-1]+nums[i])

    return max(nums)
```

Explanation: Define the maximum value of a given subarray from index 0 to i as P(i) and the original array as nums. We can easily write down the recursion function P(i) = max(nums[i], P(i-1)+nums[i]).

Time Complexity: $O(n)$, Space Complexity: $O(1)$, where n is the length of array.
