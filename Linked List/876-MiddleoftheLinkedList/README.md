# Middle of the Linked List
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given the head of a singly linked list, return the middle node of the linked list. <br><br>
If there are two middle nodes, return the second middle node.

Example 1:

![alt text](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

> Input: head = [1,2,3,4,5]\
Output: [3,4,5]\
Explanation: The middle node of the list is node 3.

Example 2:

![alt text](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

> Input: head = [1,2,3,4,5,6]\
Output: [4,5,6]\
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.


Constraints:
- The number of nodes in the list is in the range [1, 100].
- $1$ <= Node.val <= $100$

Problem can be found in [here](https://leetcode.com/problems/middle-of-the-linked-list/)!

## Solution
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### [Solution](/Linked%20List/876-MiddleoftheLinkedList/solution.py): Fast and Slow Pointers

```python
def middleNode(head: Optional[ListNode]) -> Optional[ListNode]:
    fast_pointer = slow_pointer = head

    while fast_pointer and fast_pointer.next:
        fast_pointer = fast_pointer.next.next
        slow_pointer = slow_pointer.next

    return slow_pointer
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$
