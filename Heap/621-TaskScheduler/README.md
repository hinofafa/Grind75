# Task Scheduler
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.<br><br>
However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks.<br><br>
Return the least number of units of times that the CPU will take to finish all the given tasks.

Example 1:
> Input: tasks = ["A","A","A","B","B","B"], n = 2\
Output: 8\
Explanation:\ 
A -> B -> idle -> A -> B -> idle -> A -> B\
There is at least 2 units of time between any two same tasks.

Example 2:

> Input: tasks = ["A","A","A","B","B","B"], n = 0\
Output: 6\
Explanation: On this case any permutation of size 6 would work since n = 0.\
["A","A","A","B","B","B"]\
["A","B","A","B","A","B"]\
["B","B","B","A","A","A"]\
...\
And so on.

Example 3:

> Input: tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2\
Output: 16\
Explanation: \
One possible solution is\
A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> idle -> idle -> A -> idle -> idle -> A\
 

Constraints:
- $1$ <= task.length <= $10^4$
- tasks[i] is upper-case English letter.
- The integer n is in the range [0, 100].

Problem can be found in [here](https://leetcode.com/problems/task-scheduler)!

### [Solution1](/Heap/621-TaskScheduler/solution1.py): Math & Analysis

-   This method is inspired by this [post](https://leetcode.com/problems/task-scheduler/discuss/104507/Python-Straightforward-with-Explanation).

```python
def leastInterval( tasks: List[str], n: int) -> int:
    occurrences = Counter(tasks).values()
    max_count = max(occurrences)
    num_most_frequent_tasks = list(occurrences).count(max_count)

    return max((max_count-1) * (n+1) + num_most_frequent_tasks, len(tasks))
```

Explanation: Assume that we have an example `AAABBBCCCDDD` and n=4. The most frequent tasks occur `max_count` times (3 in this example) and there are `num_most_frequent_tasks` of them (4 in this example). For easier understanding, imagine we insert tasks step by step.

1. A \_ \_ \_ _ A _ \_ \_ _ A : _ means idle time (temporary) if we cannot fill in any tasks
2. A B \_ \_ \_ A B \_ \_ \_ A B
3. A B C \_ \_ A B C \_ \_ A B C
4. A B C D \_ A B C D \_ A B C D

Notice that for the interval between any A should be at least n tasks. In other word, we can say the cycle is n+1 tasks for same task to be scheduled again (ABCD\_**A**). There will be 2 cycles (max_count-1) for scheduling all tasks in this example.

-   Why there will not be three cycles?
    -   Because we do not need the idle time for the last scheduling tasks (the last `ABCD` in this example). Therefore, it is only max_count-1 cycles.

Based on these findings, the minimum interval we need to schedule all tasks is (n+1)\*(max_count-1) + num_most_frequent_tasks. The reason why we need to add `num_most_frequent_tasks` is because we need to take the last `ABCD` into account since (n+1)\*(max_count-1) does not include the last `ABCD`.

Finally, based on the formula we only need 8 intervals for scheduling `AAABBBCDEFG` and n=2. However, we know that there are 11 tasks to be scheduled. Therefore, there should be at least 11 intervals.

Time Complexity: $O(n)$, Space Complexity: $O(n)$, where n is the length of array.

### [Solution2](/Heap/621-TaskScheduler/solution2.py): Heap

```python
def leastInterval(tasks: List[str], n: int) -> int:
    if n == 0:
        return len(tasks)

    heap = []
    occurrences = Counter(tasks).values()
    for count in occurrences:
        heapq.heappush(heap, -count)

    time, tempt = 0, []
    while heap:
        for _ in range(n+1):
            if heap or tempt:
                time += 1
            if heap:
                count = heapq.heappop(heap)
                if count < -1:
                    tempt.append(count+1)

        while tempt:
            heapq.heappush(heap, tempt.pop())

    return time
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$, where n is the length of array.
