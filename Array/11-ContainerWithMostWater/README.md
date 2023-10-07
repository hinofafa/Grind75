# Container With Most Water
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]). <br><br>
Find two lines that together with the x-axis form a container, such that the container contains the most water. <br><br>
Return the maximum amount of water a container can store. <br><br>
Notice that you may not slant the container.

 

Example 1:

![alt text](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
> Input: height = [1,8,6,2,5,4,8,3,7]\
Output: 49\
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example 2:
> Input: height = [1,1]\
Output: 1
 
Constraints:
- n == height.length
- $2$ <= n <= $10^5$
- $0$ <= height[i] <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/container-with-most-water)!

## Solution
### [Solution](/Array/11-ContainerWithMostWater/solution.py): Two Pointers

```python
def maxArea(height: List[int]) -> int:
    max_volume = 0
    left, right = 0, len(height) - 1

    while left != right:
        # if height[left] is smaller, the only way to increase volume is to check whether
        # moving left to left + 1 increase the volume since width is getting smaller.
        if height[left] >= height[right]:
            volume = height[right] * (right - left)
            right -= 1
        else:
            volume = height[left] * (right - left)
            left += 1

        max_volume = max(max_volume, volume)
    return max_volume
```

Explanation: Sorting intervals can make sure that for any 0 <= i <= size of intervals-1, intervals\[i][0]<=intervals\[i+1][0], which is a great property that we only need to change end time in overlapping cases.

Time Complexity: $O(n)$, Space Complexity: $O(1)$
