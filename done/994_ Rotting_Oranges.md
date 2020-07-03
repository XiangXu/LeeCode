#  Rotting Oranges

In a given grid, each cell can have one of three values:

* the value 0 representing an empty cell;
* the value 1 representing a fresh orange;
* the value 2 representing a rotten orange.

Every minute, any fresh orange that is adjacent (4-directionally) to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange.  If this is impossible, return -1 instead.

Example 1:

```
Input: [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

Example 2:

```
Input: [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation:  The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
```

Example 3:

```
Input: [[0,2]]
Output: 0
Explanation:  Since there are already no fresh oranges at minute 0, the answer is just 0.
```

Note:

1. 1 <= grid.length <= 10
2. 1 <= grid[0].length <= 10
3. grid[i][j] is only 0, 1, or 2.

## First Solution

Runtime: **4 ms**

Memory: **40.2 MB**

```java
class Solution 
{
    public int orangesRotting(int[][] grid) 
    {
        if(grid == null || grid.length == 0)
            return -1;
        
        int rows = grid.length;
        int columns = grid[0].length;
        int freshCount = 0;
        Queue<int[]> queue = new LinkedList<>();
        
        for(int i=0; i<rows; i++)
        {
            for(int j=0; j<columns; j++)
            {
                if(grid[i][j] == 2)
                    queue.offer(new int[] {i, j});
                else if(grid[i][j] == 1)
                    freshCount ++;
            }
        }
        
        if(freshCount == 0)
            return 0;
        
        int[][] movements = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        int step = 0;
        
        while(!queue.isEmpty())
        {
            step ++;
            int size = queue.size();
            for(int i=0; i<size; i++)
            {
                int[] rottenPoint = queue.poll();
                for(int movement[] : movements)
                {
                    int x = rottenPoint[0] + movement[0];
                    int y = rottenPoint[1] + movement[1];
                    
                    if(x < 0 || y < 0 || x >= rows || y >= columns || grid[x][y] == 0 || grid[x][y] == 2)
                        continue;
                    
                    grid[x][y] = 2;
                    queue.offer(new int[]{x, y});
                    freshCount --;
                }
            }
        }
        
        return freshCount == 0 ? step-1 : 0;
    }
}
```

**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(n)**
    