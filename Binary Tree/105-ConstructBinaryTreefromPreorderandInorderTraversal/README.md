# Construct Binary Tree from Preorder and Inorder Traversal
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

> Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]\
Output: [3,9,20,null,null,15,7]

Example 2:
> Input: preorder = [-1], inorder = [-1]\
Output: [-1]
 

Constraints:
- $1$ <= preorder.length <= $3000$
- inorder.length == preorder.length
- $-3000$ <= preorder[i], inorder[i] <= $3000$
- preorder and inorder consist of unique values.
- Each value of inorder also appears in preorder.
- preorder is guaranteed to be the preorder traversal of the tree.
- inorder is guaranteed to be the inorder traversal of the tree.

Problem can be found in [here](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)!

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/105-ConstructBinaryTreefromPreorderandInorderTraversal/solution.py):

```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        def array_to_tree(left: int, right: int) -> Optional[TreeNode]:
            nonlocal preorder_index
            if left > right:
                return None

            root_value = preorder[preorder_index]
            root_node = TreeNode(root_value)
            preorder_index += 1
            root_node.left = array_to_tree(left, inorder_map[root_value]-1)
            root_node.right = array_to_tree(inorder_map[root_value]+1, right)

            return root_node

        inorder_map = {}
        preorder_index = 0
        for index, value in enumerate(inorder):
            inorder_map[value] = index

        return array_to_tree(0, len(preorder)-1)
```

Explanation: To solve this problem, we have to use the properties of preorder and inorder traversal. We know that preorder traversal sequentially visits the root, left child, and right child. On the other hand, inorder traversal sequentially visits the left child, root, and right child. With this in mind, the root of the binary tree is the first element of the preorder traversal. For example, assume that the preorder traversla and inorder traversal of an arbitrary binary tree is [3, 9, 20, 15, 7] and [9, 3, 15, 20, 7], respectively. Then, we know that the root of that tree is 3. Since we know that the root node is 3, we can tell from the inorder traversal that elements located on the left hand side of 3 are the left subtree of the root node and elements located on the right hand side of 3 are the left subtree of the root node. In this case, 9 is in the left subtree of the root node, while [15, 20, 7] are in the right subtree of the root node. By doing so recursively, we can solve this problem.

Time Complexity: $O(n)$, Space Complexity: $O(n)$
