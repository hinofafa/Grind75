# Course Schedule
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai. <br><br>
For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1. <br><br>
Return true if you can finish all courses. Otherwise, return false.


Example 1:
> Input: numCourses = 2, prerequisites = [[1,0]]\
Output: true\
Explanation: There are a total of 2 courses to take. \
To take course 1 you should have finished course 0. So it is possible.

Example 2:
> Input: numCourses = 2, prerequisites = [[1,0],[0,1]]\
Output: false\
Explanation: There are a total of 2 courses to take. \
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Constraints:
- $1$ <= numCourses <= $2000$
- $0$ <= prerequisites.length <= $5000$
- prerequisites[i].length == $2$
- $0$ <= ai, bi < numCourses
- All the pairs prerequisites[i] are unique.

Problem can be found in [here](https://leetcode.com/problems/course-schedule)!

## Solution
### [Solution](/Graph/207-CourseSchedule/solution.py): Depth-First Search

```python
def canFinish(numCourses: int, prerequisites: List[List[int]]) -> bool:
    # Construct edges for DFS
    edges = defaultdict(list)
    for dest, src in prerequisites:
        edges[src].append(dest)

    stack = []
    node_status = [0] * numCourses          # 0: White (Not Discovered Yet), 1: Gray (Being Explored), 2: Black (Explored)
    for vertex in range(numCourses):
        stack.append(vertex)
        while stack:
            node = stack[-1]

            # The node has not been visited yet
            if node_status[node] == 0:
                node_status[node] = 1
                for neighbor in edges[node]:
                    if node_status[neighbor] == 0:
                        stack.append(neighbor)

                    # If we find a gray node, meaning that we have visited this node twice i.e. we find a cycle!
                    elif node_status[neighbor] == 1:
                        return False
                    else:
                        continue

            # In either cases, this means that we have fully explored the node. So, just simply pop the node out.
            else:
                node_status[node] = 2
                stack.pop()

    return True
```

Explanation: By performing a DFS, we can determine whether this graph is a DAG (Directed Acyclic Graph) or not. If so, we can finish all courese (should return True).

Time Complexity: $O(V+E)$, Space Complexity: $O(V+E)$, where V is the total number of courses and E is the total number of prerequisites.
