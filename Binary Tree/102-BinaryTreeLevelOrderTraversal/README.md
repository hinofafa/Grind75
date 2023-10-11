# Binary Tree Level Order Traversal
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

> Input: root = [3,9,20,null,null,15,7]\
Output: [[3],[9,20],[15,7]]

Example 2:
> Input: root = [1]\
Output: [[1]]

Example 3:
> Input: root = []\
Output: []
 

Constraints:
- The number of nodes in the tree is in the range [$0$, $2000$].
- $-1000$ <= Node.val <= $1000$

Problem can be found in [here](https://leetcode.com/problems/binary-tree-level-order-traversal)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/102-BinaryTreeLevelOrderTraversal/solution.py): Breadth-First Search

```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if root is None:
            return []

        queue, output_list = collections.deque([root]), []
        while queue:
            level = []
            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)
                if node.left is not None:
                    queue.append(node.left)
                if node.right is not None:
                    queue.append(node.right)
            output_list.append(level)

        return output_list
```

Explanation: We can solve this problem by using breadth-first search (BFS). To support performing BFS on the binary tree, we need to use a queue. As we iterate the whole binary tree, we will get the level-order traversal of given binary tree.

Time Complexity: $O(n)$, Space Complexity: $O(n)$