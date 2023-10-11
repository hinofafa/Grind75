# Serialize and Deserialize Binary Tree
![#ff0000](https://placehold.co/1x1/ff0000/ff0000.png) `Hard`

> Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment. <br><br>
Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)
> Input: root = [1,2,3,null,null,4,5]\
Output: [1,2,3,null,null,4,5]

Example 2:
> Input: root = []\
Output: []
 

Constraints:
- The number of nodes in the tree is in the range [$0$, $10^4$].
- $-1000$ <= Node.val <= $1000$

Problem can be found in [here](https://leetcode.com/problems/serialize-and-deserialize-binary-tree)!

## Solution
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### [Solution](/Binary%20Tree/297-SerializeandDeserializeBinaryTree/solution.py): Breadth-First Search

```python
class Codec:
    def serialize(self, root: Optional[TreeNode]) -> Optional[str]:
        if root is None:
            return ""

        # Perfrom BFS with queue. If a node's child is None, represent it as #.
        output_list = []
        queue = deque([root])
        while queue:
            for _ in range(len(queue)):
                node = queue.popleft()
                if node:
                    output_list.append(str(node.val))
                    queue.append(node.left)
                    queue.append(node.right)
                else:
                    output_list.append("#")

        return " ".join(output_list)

    def deserialize(self, data: str) -> Optional[TreeNode]:
        if len(data) == 0:
            return None

        i = 0
        binary_tree = data.split()
        root = TreeNode(binary_tree[0])
        queue = deque([root])
        while queue:
            # If you pop a node, its child will be at i+1 and i+2 if there is one.
            node = queue.popleft()
            i += 1
            if i < len(binary_tree) and binary_tree[i] != "#":
                node.left = TreeNode(int(binary_tree[i]))
                queue.append(node.left)

            i += 1
            if i < len(binary_tree) and binary_tree[i] != "#":
                node.right = TreeNode(int(binary_tree[i]))
                queue.append(node.right)

        return root
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$.
