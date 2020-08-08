# Sudoku Solver

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy all of the following rules:

Each of the digits 1-9 must occur exactly once in each row.
Each of the digits 1-9 must occur exactly once in each column.
Each of the the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

Note:

* The given board contain only digits 1-9 and the character '.'.
* You may assume that the given Sudoku puzzle will have a single unique solution.
* The given board size is always 9x9.

## Solution

当我看到这道题的时候我就觉得这里肯定需要使用DFS, 但是没有做出来. 看了答案以后感觉原因是因为我对数独这个游戏不太了解! 我当时想的真的是太过于复杂了.

我的理解是一个数独有很多种不同的解法, 那么我们需要尝试不同的组合, 需要记录每一个点使用过的数字. **但是其实数独的答案是唯一的, 只有一个**.

通常我们解决数独的问题是从小的3*3开始, 填入一个数字以后, 就需要做以下的三个判断:

1. 当前的行数中是否有重复的数字.
2. 当前的列数中是否有重复的数字.
3. 当前的3*3 sub box中是否有重复的数字.

这里要着重说一下第三点, 我们需要找到当前填入数字的sub box的起始点, 我们需要推导一下:

```
int startRow = 3 * (currRow / 3);
int startCol = 3 * (currCol / 3);
```

递归的方面其实还是比较好理解的.

## 空间时间复杂度分析:

* **Time Complexity: ?**
* **Space Complexity: ?**

```java
class Solution
{
    public void solveSudoku(char[][] board) 
    {
        dfs(board);
    }
    
    private boolean dfs(char[][] board)
    {
        for(int i=0; i<board.length; i++)
        {
            for(int j=0; j<board[0].length; j++)
            {
                if(board[i][j] == '.')
                {
                    for(char c='1'; c<='9'; c++)
                    {
                        if(isValid(board, i, j, c))
                        {
                            board[i][j] = c;
                            
                            if(dfs(board))
                                return true;
                            else
                                board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        
        return true;
    }
    
    
    private boolean isValid(char[][] board, int row, int col, char c)
    {
        for(int i=0; i<board.length; i++)
        {    
            // check if current column contains duplicate
            if(board[row][i] == c)
                return false;
            
            // check if current row contains duplicate
            if(board[i][col] == c)
                return false;
            
            // check if current sub box contains duplicate
            int subRow = 3 * (row / 3) + (i / 3);
            int subCol = 3 * (col / 3) + (i % 3);
            
            if(board[subRow][subCol] != '.' && board[subRow][subCol] == c)
                return false;     
        }
        
        return true;
    }
}
```