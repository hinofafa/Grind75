# Find Median from Data Stream
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard`

> The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for arr = [2,3,4], the median is 3.
- For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.

Implement the MedianFinder class:
- MedianFinder() initializes the MedianFinder object.
- void addNum(int num) adds the integer num from the data stream to the data structure.
- double findMedian() returns the median of all elements so far. Answers within $10^{-5}$ of the actual answer will be accepted.
 

Example 1:

> Input\
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]\
[[], [1], [2], [], [3], []]\
Output\
[null, null, null, 1.5, null, 2.0]\
\
Explanation\
MedianFinder medianFinder = new MedianFinder();\
medianFinder.addNum(1);    // arr = [1]\
medianFinder.addNum(2);    // arr = [1, 2]\
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)\
medianFinder.addNum(3);    // arr[1, 2, 3]\
medianFinder.findMedian(); // return 2.0
 

Constraints:
- $-10^5$ <= num <= $10^5$
- There will be at least one element in the data structure before calling findMedian.
- At most $5 * 10^4$ calls will be made to addNum and findMedian.
 

Follow up:

If all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?
If 99% of all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?

Problem can be found in [here](https://leetcode.com/problems/find-median-from-data-stream)!

### [Solution](/Heap/295-FindMedianfromDataStream/solution.py): Heap

```python
class MedianFinder:
    def __init__(self):
        self.min_heap, self.max_heap = [], []

    def addNum(self, num: int) -> None:
        if len(self.min_heap) < len(self.max_heap):
            heappush(self.min_heap, -heappushpop(self.max_heap, -num))
        else:
            heappush(self.max_heap, -heappushpop(self.min_heap, num))

    def findMedian(self) -> float:
        if len(self.min_heap) == len(self.max_heap):
            return (self.min_heap[0] - self.max_heap[0]) / 2
        else:
            return -self.max_heap[0]
```

Time Complexity: $O(logn)$ for adding new number and O(1) for finding the median number, Space Complexity: $O(n)$, where n is the number of numbers.
