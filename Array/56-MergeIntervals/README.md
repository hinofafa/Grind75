# Merge Intervals
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> Given an array of intervals where intervals[i] = [$start_i$, $end_i$], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:
> Input: intervals = [[1,3],[2,6],[8,10],[15,18]]\
Output: [[1,6],[8,10],[15,18]]\
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

Example 2:
> Input: intervals = [[1,4],[4,5]]\
Output: [[1,5]]\
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 
Constraints:
- $1$ <= intervals.length <= $10^4$
- intervals[i].length == $2$
- $0$ <= $start_i$ <= $end_i$ <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/merge-intervals/)!

## Solution
### [Solution](/Array/56-MergeIntervals/solution.py): Sorting

```python
def merge(intervals: List[List[int]]) -> List[List[int]]:
    # Sorting intervals can make sure that i.start <= i+1.start
    intervals.sort()
    output_list = [intervals[0]]

    for i in range(1, len(intervals)):
        # No Overlapping Case
        if output_list[-1][1] < intervals[i][0]:
            output_list.append(intervals[i])
        # Overlapping Case
        else:
            output_list[-1][1] = max(output_list[-1][1], intervals[i][1])

    return output_list
```

Explanation: Sorting intervals can make sure that for any 0 <= i <= size of intervals-1, intervals\[i][0]<=intervals\[i+1][0], which is a great property that we only need to change end time in overlapping cases.

Time Complexity: $O(nlogn)$, Space Complexity: $O(1)$
