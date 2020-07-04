# Number of Islands

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

```
Input:
11110
11010
11000
00000

Output: 1
```

Example 2:

```
Input:
11000
11000
00100
00011

Output: 3
```

## First Solution - Depth First Search DFS

Runtime: **2 ms**

Memory: **44.5 MB**

```java
class Solution 
{
    public int numIslands(char[][] grid)
    {
        int count = 0;
       
        if(grid == null || grid.length == 0)
            return count;
        
        for(int i=0; i<grid.length; i++)
        {
            for(int j=0; j<grid[0].length; j++)
            {
                if(grid[i][j] == '1')
                {
                    count ++;
                    findLands(grid, i, j);
                }
            }
        }
        
        return count;
    }
    
    public void findLands(char[][] grid, int i, int j)
    {
        if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0')
            return;
        
        grid[i][j] = '0';

        findLands(grid, i+1, j);
        findLands(grid, i-1, j);
        findLands(grid, i, j+1);
        findLands(grid, i, j-1);
    }
}
``` 

**Time Complexity: O(n)**

**Space Complexity: O(n)**