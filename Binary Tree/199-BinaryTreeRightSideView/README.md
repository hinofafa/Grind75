# Binary Tree Right Side View
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.


Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

> Input: root = [1,2,3,null,5,null,4]\
Output: [1,3,4]

Example 2:

> Input: root = [1,null,3]\
Output: [1,3]

Example 3:

> Input: root = []\
Output: []
 

Constraints:
- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

Problem can be found in [here](https://leetcode.com/problems/binary-tree-right-side-view)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/199-BinaryTreeRightSideView/solution.py): Breadth-First Search

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if root is None:
            return []

        output_list = []
        queue = deque([root])
        while queue:
            temp = []
            for _ in range(len(queue)):
                node = queue.popleft()
                temp.append(node.val)
                if node.left is not None:
                    queue.append(node.left)
                if node.right is not None:
                    queue.append(node.right)
            output_list.append(temp[-1])

        return output_list
```

Explanation: This problem is basically the same as [Leetcode 102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal). Instead of appending the whole array, we just need to append the last element to the output array.

Time Complexity: $O(n)$, Space Complexity: $O(n)$
