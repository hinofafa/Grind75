# Insert Interval
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> You are given an array of non-overlapping intervals **intervals** where **intervals[i] = [$start_i$, $end_i$]** represent the start and the end of the *$i^{th}$* interval and intervals is sorted in ascending order by $start_i$. You are also given an interval **newInterval = [start, end]** that represents the start and end of another interval. <br><br>
Insert **newInterval** into **intervals** such that **intervals** is still sorted in ascending order by **$start_i$** and **intervals** still does not have any overlapping intervals (merge overlapping intervals if necessary). <br><br>
Return **intervals** after the insertion.

Example 1:
> Input: intervals = [[1,3],[6,9]], newInterval = [2,5]\
Output: [[1,5],[6,9]]

Example 2:
> Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]\
Output: [[1,2],[3,10],[12,16]]\
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

Constraints:
- $0$ <= intervals.length <= $10^4$
- intervals[i].length == $2$
- $0$ <= starti <= endi <= $10^5$
- intervals is sorted by $start_i$ in ascending order.
- newInterval.length == $2$
- $0$ <= start <= end <= $10^5$

Problem can be found in [here](https://leetcode.com/problems/insert-interval)!

## Solution
### [Solution](/Array/57-InsertInterval/solution.py)

```python
def insert(intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
    output_list = []
    for counter, interval in enumerate(intervals):
        if interval[1] < newInterval[0]:                   # No intersection of two intervals
            output_list.append(interval)
        elif interval[0] > newInterval[1]:
            output_list.append(newInterval)
            return output_list + intervals[counter:]
        else:                                              # Overlap Cases
            new_start_time = min(interval[0], newInterval[0])
            new_end_time = max(interval[1], newInterval[1])
            newInterval = [new_start_time, new_end_time]
    output_list.append(newInterval)

    return output_list
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$