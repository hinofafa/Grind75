# Flood Fill
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image. <br><br>
You are also given three integers sr, sc, and color. You should perform a flood fill on the image starting from the pixel image[sr][sc].<br><br>
To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with color.<br><br>
Return the modified image after performing the flood fill.

Example 1:

![alt image](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

> Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2\
Output: [[2,2,2],[2,2,0],[2,0,1]]\
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.\
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.

Example 2:
> Input: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, color = 0\
Output: [[0,0,0],[0,0,0]]\
Explanation: The starting pixel is already colored 0, so no changes are made to the image.
 

Constraints:
- m == image.length
- n == image[i].length
- $1$ <= m, n <= $50$
- $0$ <= image[i][j], color < $2^{16}$
- $0$ <= sr < m
- $0$ <= sc < n

Problem can be found in [here](https://leetcode.com/problems/flood-fill)!

## Solution
### [Solution](/Graph/733-FloodFill/solution.py): Depth-First Search

```python
def floodFill(image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
    def search_and_fill(row: int, column: int) -> None:
        if image[row][column] == previos_color:
            image[row][column] = color
            if row + 1 < number_of_rows:
                search_and_fill(row+1, column)
            if row >= 1:
                search_and_fill(row-1, column)
            if column + 1 < number_of_columns:
                search_and_fill(row, column+1)
            if column >= 1:
                search_and_fill(row, column-1)

    number_of_columns, number_of_rows = len(image[0]), len(image)
    previos_color = image[sr][sc]
    if previos_color == color:
        return image

    search_and_fill(sr, sc)
    return image
```

Explanation: To solve this problem, we need to perform depth-first search (DFS). Notice that when we need to search in 4 directions, we need to check whether exceeeds the boundaries.

Time Complexity: $O(m*n)$, Space Complexity: $O(m*n)$ for recursion stack, where m is the number of row and n is the number of column.
