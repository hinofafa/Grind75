# Minimum Height Trees
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree. <br><br>
Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs). <br><br>
Return a list of all MHTs' root labels. You can return the answer in any order. <br><br>
The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.


Example 1:

![alt image](https://assets.leetcode.com/uploads/2020/09/01/e1.jpg)

> Input: n = 4, edges = [[1,0],[1,2],[1,3]]\
Output: [1]\
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.

Example 2:

![alt image](https://assets.leetcode.com/uploads/2020/09/01/e2.jpg)

> Input: n = 6, edges = [[3,0],[3,1],[3,2],[3,4],[5,4]]\
Output: [3,4]

Constraints:
- $1$ <= $n$ <= $2 * 10^4$
- edges.length == $n - 1$
- $0$ <= $a_i$, $b_i$ < $n$
- $a_i$ != $b_i$
- All the pairs (ai, bi) are distinct.
- The given input is guaranteed to be a tree and there will be no repeated edges.

Problem can be found in [here](https://leetcode.com/problems/minimum-height-trees)!

### [Solution](/Graph/310-MinimumHeightTrees/solution.py): Topological Sort

```python
def findMinHeightTrees(n: int, edges: List[List[int]]) -> List[int]:
    # Edge Cases: only one node in the graph
    if not edges:
        return [0]

    # Build up adjacency list
    adjacency_list = [set() for _ in range(n)]
    for start, end in edges:
        adjacency_list[start].add(end)
        adjacency_list[end].add(start)

    # Find the leaf nodes of the tree
    leaves = []
    for index, neighbors in enumerate(adjacency_list):
        if len(neighbors) == 1:
            leaves.append(index)

    # Remove leaf nodes until there is less than or equal to 2 nodes
    leaf_reamining = n
    while leaf_reamining > 2:
        new_leaves = []
        leaf_reamining -= len(leaves)
        for _ in range(len(leaves)):
            leaf_node = leaves.pop()
            neighbor = adjacency_list[leaf_node].pop()
            adjacency_list[neighbor].remove(leaf_node)
            if len(adjacency_list[neighbor]) == 1:
                new_leaves.append(neighbor)
        leaves = new_leaves

    return leaves
```

Time Complexity: $O(N)$, Space Complexity: $O(N)$, where N is the number of nodes.
