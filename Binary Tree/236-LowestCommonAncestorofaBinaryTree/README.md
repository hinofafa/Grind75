# Lowest Common Ancestor of a Binary Tree
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.<br><br>
According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”
 

Example 1:

![alt image](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1\
Output: 3\
Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:

![alt image](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4\
Output: 5\
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

Example 3:
> Input: root = [1,2], p = 1, q = 2
Output: 1
 

Constraints:
- The number of nodes in the tree is in the range [$2$, $10^5$].
- $-10^9$ <= Node.val <= $10^9$
- All Node.val are unique.
- p != q
- p and q will exist in the tree.

Problem can be found in [here](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/236-LowestCommonAncestorofaBinaryTree/solution.py): Depth-First Search

```python
class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        # Case 1: We have reached the children of leaf node
        if root is None:
            return root
        # Case 2: Found the targeted tree node
        if root == p or root == q:
            return root

        # Search for targeted tree nodes
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        # If both targeted tree nodes are found, then return
        if left and right:
            return root
        # There are two scenarios: either one of the children found the targeted node and neither of them found.
        # For the first case: if we find p in left subtree and q is not found, this means that q is the child of p.
        # Therefore, we should return p as the lowest common ancestor.
        else:
            return left or right
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$