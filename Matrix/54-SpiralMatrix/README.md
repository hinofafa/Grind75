# Spiral Matrix
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an m x n matrix, return all elements of the matrix in spiral order.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

> Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]\
Output: [1,2,3,6,9,8,7,4,5]

Example 2:

![alt image](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

> Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]\
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
 

Constraints:
- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 10
- $-100$ <= matrix[i][j] <= $100$

Problem can be found in [here](https://leetcode.com/problems/spiral-matrix)!

### [Solution](/Matrix/54-SpiralMatrix/solution.py): Matrix Manipulation

```python
def spiralOrder(matrix: List[List[int]]) -> List[int]:
    output_list = []
    top, bottom = 0, len(matrix)-1
    left, right = 0, len(matrix[0])-1

    while top < bottom and left < right:
        for column in range(left, right):
            output_list.append(matrix[top][column])

        for row in range(top, bottom):
            output_list.append(matrix[row][right])

        for column in range(right, left, -1):
            output_list.append(matrix[bottom][column])

        for row in range(bottom, top, -1):
            output_list.append(matrix[row][left])

        top, bottom, left, right = top+1, bottom-1, left+1, right-1

    for row in range(top, bottom+1):
        for column in range(left, right+1):
            output_list.append(matrix[row][column])

    return output_list
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$, where n is the number of elements in $matrix$.
