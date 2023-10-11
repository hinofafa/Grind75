# Linked List Cycle
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given head, the head of a linked list, determine if the linked list has a cycle in it. <br><br>
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter. <br><br>
Return true if there is a cycle in the linked list. Otherwise, return false.


Example 1:

![alt text](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)
> Input: head = [3,2,0,-4], pos = 1\
Output: true\
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:

![alt text](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)
> Input: head = [1,2], pos = 0\
Output: true\
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:

![alt text](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)
> Input: head = [1], pos = -1\
Output: false\
Explanation: There is no cycle in the linked list.
 

Constraints:
- The number of the nodes in the list is in the range [$0$, $104$].
- $-105$ <= Node.val <= $105$
- pos is $-1$ or a valid index in the linked-list.
 

Follow up: Can you solve it using $O(1)$ (i.e. constant) memory?

Problem can be found in [here](https://leetcode.com/problems/linked-list-cycle/)!

## Solution
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### [Solution](/Linked%20List/141-LinkedListCycle/solution.py): Fast Slow Pointers

```python
def hasCycle(head: Optional[ListNode]) -> bool:
    fast_pointer = slow_pointer = head

    while fast_pointer and fast_pointer.next:
        fast_pointer, slow_pointer = fast_pointer.next.next, slow_pointer.next
        if fast_pointer == slow_pointer:
            return True

    return False
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$