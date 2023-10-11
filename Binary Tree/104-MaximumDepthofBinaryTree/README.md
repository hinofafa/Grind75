# Maximum Depth of Binary Tree
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given the root of a binary tree, return its maximum depth. <br><br>
A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

> Input: root = [3,9,20,null,null,15,7]\
Output: 3

Example 2:
> Input: root = [1,null,2]\
Output: 2
 

Constraints:
- The number of nodes in the tree is in the range [$0$, $10^4$].
- $-100$ <= Node.val <= $100$

Problem can be found in [here](https://leetcode.com/problems/maximum-depth-of-binary-tree)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/104-MaximumDepthofBinaryTree/solution.py): Depth-First Search

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0

        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```

Explanation: If we want to find out the maximum depth of an arbitrary binary tree node, we need to calculate the depth of its left child and right child. Therefore, to return the depth of a binary tree, we just need to iterate from the top of root to the leaf.

Time Complexity: $O(n)$, Space Complexity: $O(h)$ for the recursive stack, where h is the height of the binary tree. In worst case, h will be n for an unbalanced binary tree.
