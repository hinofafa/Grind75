# Diameter of Binary Tree
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given the root of a binary tree, return the length of the diameter of the tree. <br><br>
The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root. <br><br>
The length of a path between two nodes is represented by the number of edges between them.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

> Input: root = [1,2,3,4,5]\
Output: 3\
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].

Example 2:
> Input: root = [1,2]\
Output: 1
 
Constraints:
- The number of nodes in the tree is in the range [1, $10^4$].
- $-100$ <= Node.val <= $100$

Problem can be found in [here](https://leetcode.com/problems/diameter-of-binary-tree)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/543-DiameterofBinaryTree/solution.py): Depth-First Search

```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.answer = 0
        self.find_diameter(root)
        return self.answer

    def find_diameter(self, node: Optional[TreeNode]) -> int:
        # The reason to return -1 is to compensate for the addition of 2 in the following lines
        if node is None:
            return -1

        left, right = self.find_diameter(node.left), self.find_diameter(node.right)
        # We need to add 2 for calculating the diameter is because
        # we need to count the path from left and right subtrees to root, respectively.
        self.answer = max(self.answer, 2+left+right)
        return 1 + max(left, right)
```

Explanation: The intuitive solution is to check "every" tree node to calculate the diameter of a binary tree. However, the algorithm will run in $O(n^2)$ time, which sucks. To improve the algorithm's time complexity, we can perform a depth-first search (DFS) to store the previous result through recursion.

Time Complexity: $O(n)$, Space Complexity: $O(h)$ for the recursive stack, where h is the height of the binary tree. In worst case, h will be n for an unbalanced binary tree. Therefore, the space complexity will be $O(n)$.
