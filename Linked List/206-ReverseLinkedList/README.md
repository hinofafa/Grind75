# Reverse Linked List
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:

![alt text](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

> Input: head = [1,2,3,4,5]\
Output: [5,4,3,2,1]

Example 2:

![alt text](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

> Input: head = [1,2]\
Output: [2,1]

Example 3:

> Input: head = []\
Output: []
 

Constraints:
- The number of nodes in the list is the range [0, 5000].
- $-5000$ <= Node.val <= $5000$
 

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

Problem can be found in [here](https://leetcode.com/problems/reverse-linked-list/)!

## Solution
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### [Solution](/Linked%20List/206-Reverse-Linked-List/solution.py)

```python
def reverseList(head: Optional[ListNode]) -> Optional[ListNode]:
    previous_node = None
    while head:
        current_node = head
        head = head.next
        current_node.next = previous_node
        previous_node = current_node

    return previous_node
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$