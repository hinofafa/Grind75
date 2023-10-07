# Largest Rectangle in Histogram
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard` 

> Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

Example 1:

![alt text](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)
> Input: heights = [2,1,5,6,2,3]\
Output: 10\
Explanation: The above is a histogram where width of each bar is 1.\
The largest rectangle is shown in the red area, which has an area = 10 units.

Example 2:

![alt text](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)
> Input: heights = [2,4]\
Output: 4
 

Constraints:
- $1$ <= heights.length <= $10^5$
- $0$ <= heights[i] <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/largest-rectangle-in-histogram)!

## Solution
### [Solution](/Stack/84-LargestRectangleinHistogram/solution.py): Stack

```python
def largestRectangleArea(heights: List[int]) -> int:
    stack = [-1]
    largest_area = 0
    heights.append(-1)

    for index, height in enumerate(heights):
        while stack and heights[stack[-1]] > height:
            current_height = heights[stack.pop()]
            current_width = index - stack[-1] - 1
            current_area = current_height * current_width
            largest_area = max(current_area, largest_area)

        stack.append(index)

    return largest_area
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$
