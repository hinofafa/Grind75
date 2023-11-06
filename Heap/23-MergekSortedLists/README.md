# Merge k Sorted Lists
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard`

> You are given an array of k linked-lists lists, each linked-list is sorted in ascending order. <br><br>
Merge all the linked-lists into one sorted linked-list and return it.

Example 1:
> Input: lists = [[1,4,5],[1,3,4],[2,6]]\
Output: [1,1,2,3,4,4,5,6]\
Explanation: The linked-lists are:\
[\
  1->4->5,\
  1->3->4,\
  2->6\
]\
merging them into one sorted list:\
1->1->2->3->4->4->5->6

Example 2:
> Input: lists = []\
Output: []

Example 3:
> Input: lists = [[]]\
Output: []

Constraints:
- k == lists.length\
- $0$ <= k <= $10^4$
- $0$ <= lists[i].length <= $500$
- $-10^4$ <= lists[i][j] <= $10^4$
- lists[i] is sorted in ascending order.
- The sum of lists[i].length will not exceed $10^4$.

Problem can be found in [here](https://leetcode.com/problems/merge-k-sorted-lists)!

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### [Solution](/Heap/23-MergekSortedLists/solution.py): Heap

```python
def mergeKLists(lists: List[Optional[ListNode]]) -> Optional[ListNode]:
    if lists is None:
        return []

    heap = []
    for i in lists:
        if i is not None:
            heappush(heap, (i.val, id(i), i))

    dummy_head = current = ListNode()
    while heap:
        node = heappop(heap)[2]
        current.next = current = node
        if node.next:
            next_node = node.next
            heappush(heap, (current.val, id(next_node), next_node))

    return dummy_head.next
```

Time Complexity: $O(nlogk)$, Space Complexity: $O(k)$, where n is the number of nodes in all linked lists and k is the number of linked lists.
