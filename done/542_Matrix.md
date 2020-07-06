# Matrix

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

Example 1:

```
Input:
[[0,0,0],
 [0,1,0],
 [0,0,0]]

Output:
[[0,0,0],
 [0,1,0],
 [0,0,0]]
```

Example 2:

```
Input:
[[0,0,0],
 [0,1,0],
 [1,1,1]]

Output:
[[0,0,0],
 [0,1,0],
 [1,2,1]]
```

Note:

1. The number of elements of the given matrix will not exceed 10,000.
2. There are at least one 0 in the given matrix.
3. The cells are adjacent in only four directions: up, down, left and right

## First Solution

Runtime: **14 ms**

Memory: **41.2 MB**


```java
class Solution 
{
    public int[][] updateMatrix(int[][] matrix) 
    {
        if(matrix == null || matrix.length == 0)
            return matrix;
        
        int rows = matrix.length;
        int columns = matrix[0].length;
        boolean[][] visited = new boolean[rows][columns];
        Queue<int[]> queue = new LinkedList<>();
        
        for(int i=0; i<rows; i++)
        {
            for(int j=0; j<columns; j++)
            {
                if(matrix[i][j] == 0)
                {
                    queue.offer(new int[]{i, j});
                    visited[i][j] = true;
                }
            }
                    
        }
        
        int[][] directions = { {1, 0}, {-1, 0}, {0, 1}, {0, -1} };
        while(!queue.isEmpty())
        {
            int[] point = queue.poll();
            for(int[] direction : directions)
            {
                int x = point[0] + direction[0];
                int y = point[1] + direction[1];
                
                if(x < 0 || x >= rows || y < 0 || y >= columns || visited[x][y] || matrix[x][y] == 0)
                    continue;
                
                visited[x][y] = true;
                queue.offer(new int[]{x, y});
                matrix[x][y] += matrix[point[0]][point[1]];
            }
        }
        
        return matrix;
    }
}
```


**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(n)**