# Maximum Profit in Job Scheduling
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard`

> We have n jobs, where every job is scheduled to be done from startTime[i] to endTime[i], obtaining a profit of profit[i].<br><br>
You're given the startTime, endTime and profit arrays, return the maximum profit you can take such that there are no two jobs in the subset with overlapping time range.<br><br>
If you choose a job that ends at time X you will be able to start another job that starts at time X.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2019/10/10/sample1_1584.png)

> Input: startTime = [1,2,3,3], endTime = [3,4,5,6], profit = [50,10,40,70]\
Output: 120\
Explanation: The subset chosen is the first and fourth job. \
Time range [1-3]+[3-6] , we get profit of 120 = 50 + 70.

Example 2:

![alt image](https://assets.leetcode.com/uploads/2019/10/10/sample22_1584.png)

> Input: startTime = [1,2,3,4,6], endTime = [3,5,10,6,9], profit = [20,20,100,70,60]\
Output: 150\
Explanation: The subset chosen is the first, fourth and fifth job.\
Profit obtained 150 = 20 + 70 + 60.

Example 3:

![alt image](https://assets.leetcode.com/uploads/2019/10/10/sample3_1584.png)

> Input: startTime = [1,1,1], endTime = [2,3,4], profit = [5,6,4]\
Output: 6

Constraints:
- $1$ <= startTime.length == endTime.length == profit.length <= $5 * 10^4$
- $1$ <= startTime[i] < endTime[i] <= $10^9$
- $1$ <= profit[i] <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/maximum-profit-in-job-scheduling)!

## Solution
### [Solution](/Binary%20Search/1235-MaximumProfitinJobScheduling/solution.py): Dynamic Programming

```python
# Support Memorization for Dynamic Programming
def memorization(func):
    memo = {}

    def helper(x):
        if x not in memo:
            memo[x] = func(x)
        return memo[x]
    return helper


class Solution:
    def jobScheduling(self, startTime: List[int], endTime: List[int], profit: List[int]) -> int:
        def find_next_available_job(index: int, end_time: int) -> int:
            # Perform the binary search to find the smallest next available job i for the current job j
            # such that j.endtime <= i.starttime. If none, return the number of jobs.

            left, right = index, len(jobs)
            while left < right:
                mid = left + (right-left) // 2
                if jobs[mid][0] >= end_time:
                    right = mid
                else:
                    left = mid + 1

            return left

        @memoization
        def find_optimal_schedule(index: int) -> int:
            if index == len(jobs):
                return 0
            next_available_job = find_next_available_job(index, jobs[index][1])

            # Defined the maximum profit for interval 1 to j as OPT(j) => OPT(j) = max{j.profit + OPT(p(j)), OPT(j-1)}
            # where p(j) is the next available job for job j
            max_profit = max(jobs[index][2]+find_optimal_schedule(next_available_job), find_optimal_schedule(index+1))
            return max_profit

        jobs = sorted(zip(startTime, endTime, profit))
        return find_optimal_schedule(0)
```

Time Complexity: $O(nlogn)$, Space Complexity: $O(n)$