# Lowest Common Ancestor of a Binary Search Tree
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST. <br><br>
According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Example 1:

![alt image](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

> Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8\
Output: 6\
Explanation: The LCA of nodes 2 and 8 is 6.

Example 2:

![alt image](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

> Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4\
Output: 2\
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

Example 3:

> Input: root = [2,1], p = 2, q = 1\
Output: 2
 

Constraints:
- The number of nodes in the tree is in the range [$2$, $10^5$].
- $-10^9$ <= Node.val <= $10^9$
- All Node.val are unique.
- p != q
- p and q will exist in the BST.

Problem can be found in [here](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree)!

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Search%20Tree/235-LowestCommonAncestorofaBinarySearchTree/solution.py): Depth-First Search

```python
def lowestCommonAncestor(root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
    max_value, min_value = max(p.val, q.val), min(p.val, q.val)
    while root:
        if root.val > max_value:
            root = root.left
        elif root.val < min_value:
            root = root.right
        else:
            return root
```

Explanation: You can use the same [solution](/Binary%20Tree/236-LowestCommonAncestorofaBinaryTree/) to solve this problem. However, we can improve our time complexity by considering the properties of binary search tree, which is value on the left subtree's nodes < root's value < value on the right subtree's nodes.

Time Complexity: $O(h)$, Space Complexity: $O(1)$, where h is the height of the binary search tree.
