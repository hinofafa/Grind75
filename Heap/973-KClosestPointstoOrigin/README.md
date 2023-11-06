# K Closest Points to Origin
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an array of points where points[i] = [$x_i$, $y_i$] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0). <br><br>
The distance between two points on the X-Y plane is the Euclidean distance (i.e., $\sqrt((x_1 - x_2)^2 + (y_1 - y_2)^2)$). <br><br>
You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

> Input: points = [[1,3],[-2,2]], k = 1\
Output: [[-2,2]]\
Explanation:\
The distance between (1, 3) and the origin is sqrt(10).\
The distance between (-2, 2) and the origin is sqrt(8).\
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.\
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].

Example 2:

> Input: points = [[3,3],[5,-1],[-2,4]], k = 2\
Output: [[3,3],[-2,4]]\
Explanation: The answer [[-2,4],[3,3]] would also be accepted.
 

Constraints:
- $1$ <= k <= points.length <= $10^4$
- $-10^4$ <= $x_i$, $y_i$ <= $10^4$

Problem can be found in [here](https://leetcode.com/problems/k-closest-points-to-origin)!

### [Solution1](/Heap/973-KClosestPointstoOrigin/solution1.py): Heap

```python
def kClosest(points: List[List[int]], k: int) -> List[List[int]]:
    heap = [(-euclidean_distance(points[i]), points[i]) for i in range(k)]
    heapq.heapify(heap)

    for i in range(k, len(points)):
        distance = -self.euclidean_distance(points[i])
        if distance > heap[0][0]:
            heapq.heappushpop(heap, (distance, points[i]))

    return [point for _, point in heap]

def euclidean_distance(point: List[int]):
    return pow(point[0], 2) + pow(point[1], 2)
```

Explanation: Since the problem is asking us to return k closest points to the origin, we can construct a heap with the first k points in the array points. After that we can iterate the remaining array, if we find the distance is larger than smallest value in the heap (notice that there is a negative sign, so smaller value indicates farther distance from the point to the origin), we can pop that value out and push the point in.

Time Complexity: $O(nlogk)$, Space Complexity: $O(k)$, where n is the length of array and k is the number of closest points to the origin we need to return.

### [Solution2](/Heap/973-KClosestPointstoOrigin/solution2.py): Binary Search

```python
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        self.remaining_points = list(range(len(points)))
        self.distances = [self.squared_distance(point) for point in points]

        closest_points = []
        low, high = 0, max(self.distances)
        while k:
            mid = (low+high) / 2
            self.binary_search(mid)
            if len(self.closer) > k:
                self.remaining_points = self.closer
                high = mid
            else:
                low = mid
                k -= len(self.closer)
                self.remaining_points = self.farther
                closest_points.extend(self.closer)

        return [points[i] for i in closest_points]

    def binary_search(self, threshold: int):
        self.closer, self.farther = [], []
        for i in self.remaining_points:
            if self.distances[i] > threshold:
                self.farther.append(i)
            else:
                self.closer.append(i)

    def squared_distance(self, point: List[int]):
        return pow(point[0], 2) + pow(point[1], 2)

```

Time Complexity: $O(n)$, Space Complexity: $O(n)$, where n is the length of array.
