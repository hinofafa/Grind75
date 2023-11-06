# Kth Smallest Element in a BST
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

> Input: root = [3,1,4,null,2], k = 1\
Output: 1

Example 2:

![alt image](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

> Input: root = [5,3,6,2,4,null,null,1], k = 3\
Output: 3

Constraints:
- The number of nodes in the tree is n.
- $1$ <= k <= n <= $10^4$
- $0$ <= Node.val <= $10^4$
 

Follow up: If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

Problem can be found in [here](https://leetcode.com/problems/kth-smallest-element-in-a-bst)!

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Search%20Tree/230-KthSmallestElementinaBST/solution.py): Depth-First Search

```python
def kthSmallest(root: Optional[TreeNode], k: int) -> int:
    stack = []

    while True:
        while root:
            stack.append(root)
            root = root.left

        root = stack.pop()
        k -= 1
        if not k:
            return root.val
        root = root.right
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$, where n is the number of treenodes in the binary search tree.
