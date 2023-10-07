# Trapping Rain Water
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard` 

> Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

Example 1:

![alt text](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

> Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]\
Output: 6\
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

Example 2:
> Input: height = [4,2,0,3,2,5]\
Output: 9
 

Constraints:
- n == height.length
- $1$ <= n <= $2 * 10^4$
- $0$ <= height[i] <= $10^5$

Problem can be found in [here](https://leetcode.com/problems/trapping-rain-water)!

## Solution
### [Solution1](/Stack/42-TrappingRainWater/solution1.py): Dynamic Programming

```python
def trap(height: List[int]) -> int:
    volumne = 0
    left_max, right_max = [0], [0]*len(height)
    left_max[0], right_max[-1] = height[0], height[-1]

    for i in range(1, len(height)):
        left_max.append(max(left_max[-1], height[i]))

    for i in range(len(height)-2, -1, -1):
        right_max[i] = max(right_max[i+1], height[i])

    for i in range(len(height)):
        volumne += min(left_max[i], right_max[i]) - height[i]

    return volumne
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$

### [Solution2](/Stack/42-TrappingRainWater/solution2.py): Two Pointers

```python
def trap(height: List[int]) -> int:
    left, right = 0, len(height)-1
    left_max = right_max = volumne = 0
    while left <= right:
        if left_max <= right_max:
            volumne += max(left_max - height[left], 0)
            left_max = max(left_max, height[left])
            left += 1
        else:
            volumne += max(right_max - height[right], 0)
            right_max = max(right_max, height[right])
            right -= 1

    return volumne
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$

### [Solution3](/Stack/42-TrappingRainWater/solution3.py): Stack

```python
def trap(height: List[int]) -> int:
    stack = []
    volumne = 0

    for i in range(len(height)):
        while stack and height[i] > height[stack[-1]]:
            candidate = height[stack.pop()]
            if stack:
                bounded_height = min(height[i], height[stack[-1]]) - candidate
                width = i - stack[-1] - 1
                volumne += bounded_height * width

        stack.append(i)

    return volumne
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$