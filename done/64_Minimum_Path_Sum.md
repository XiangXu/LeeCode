# Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

## First Solution - DFS Time Limit Exceeded

```java
class Solution 
{
    public int minPathSum(int[][] grid) 
    {
        if(grid == null || grid.length == 0)
            return 0;
        
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        
        getPathSum(grid, 0, 0, 0, queue);
        
        return queue.isEmpty() ? 0 : queue.poll();
    }
    
    public void getPathSum(int[][] grid, int row, int column, int pathSum, PriorityQueue<Integer> queue)
    {           
        if(row >= grid.length || column >= grid[0].length || (!queue.isEmpty() && pathSum >= queue.peek()))
            return;
        
        pathSum += grid[row][column];
        if(row == grid.length-1 && column == grid[0].length-1){
            queue.offer(pathSum);
        }
        getPathSum(grid, row+1, column, pathSum, queue);
        getPathSum(grid, row, column+1, pathSum, queue);
            
    }
}
```

## Second Solution - BFS

Runtime: **29 ms**

Memory: **45 MB**

```java
class Solution 
{
    public int minPathSum(int[][] grid) 
    {
        if(grid == null || grid.length == 0)
            return 0;
        
        int rows = grid.length;
        int columns = grid[0].length;
        
        boolean[][] visited = new boolean[rows][columns];
        int[][] directions = { {1, 0}, {0, 1} };
      
        Queue<int[]> queue = new PriorityQueue<int[]>((a,b) -> a[2] - b[2]);
        queue.offer(new int[]{0, 0, grid[0][0]});

        while(!queue.isEmpty())
        {
            int[] point = queue.poll();
            
            System.out.println("value: " + grid[point[0]][point[1]] + " number: " + point[2]);
            
            for(int[] direction : directions)
            {
                int x = point[0] + direction[0];
                int y = point[1] + direction[1];
             
                if(x >= rows || y >= columns || visited[x][y] == true)
                    continue;

                visited[x][y] = true;
                int next[] = new int[]{x, y, point[2] + grid[x][y]};
               
                if(x == rows-1 &&  y == columns-1){
                    return next[2];
                }
                queue.offer(next);
            }
            
        }
        
        return grid[0][0];
    }
}
```

**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(n)**