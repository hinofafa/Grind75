# Merge Two Sorted Lists
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> You are given the heads of two sorted linked lists list1 and list2. <br><br>
Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists. <br><br>
Return the head of the merged linked list.

![alt text](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

Example 1:
> Input: list1 = [1,2,4], list2 = [1,3,4]\
Output: [1,1,2,3,4,4]

Example 2:
> Input: list1 = [], list2 = []\
Output: []

Example 3:
> Input: list1 = [], list2 = [0]\
Output: [0]

Constraints:
- The number of nodes in both lists is in the range [0, 50].
- $-100$ <= Node.val <= $100$
- Both list1 and list2 are sorted in non-decreasing order.

Problem can be found in [here](https://leetcode.com/problems/merge-two-sorted-lists)!

## Solutions
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### [Solution](/Linked%20List/21-Merge-Two-Sorted-Lists/solution.py): Dummy Head

```python
def mergeTwoLists(list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
    dummy_head = current_node = ListNode()

    while list1 and list2:
        if list1.val < list2.val:
            current_node.next = list1
            list1 = list1.next
        else:
            current_node.next = list2
            list2 = list2.next
        current_node = current_node.next

    current_node.next = list1 if list1 else list2
    return dummy_head.next
```

Time Complexity: $O(n+m)$, Space Complexity: $O(1)$, where n and m are the length of list1 and list2, respectively.
