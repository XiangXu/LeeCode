# N-Queens

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

Example:

```
Input: 4
Output: [
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above.
```

## Solution

## 空间时间复杂度分析:

* **Time Complexity: O(N<sup>2</sup>)**
* **Space Complexity: O(N)**

这道题题目的意思是要将Queen放入棋牌中且上下左右并且对角线都不能有相邻的连个Queen在一起, 那么思考一下就会发现这里需要用backtracking来解决.

具体的思路其实就是尝试在每一个位置放入Q然后看是不是满足题意, 如果满足进行下一row, 不然的话就退回上一步.

为了更好的解决问题我们需要创建一个二维数组来board记录Queen的位置, 我们可以之后将board转换为list来当做答案返回.

```java
class Solution 
{
    public List<List<String>> solveNQueens(int n) 
    {
        // handle special case
        if(n <= 0)
            return Collections.emptyList();
    
        List<List<String>> result = new ArrayList<>();
        
        // use a 2-D array to represent board, we will convert it back to list reuslt later.
        char[][] board = generateBoard(n);
        
        backTracking(result, board, 0);
        
        return result;
    }
    
    private void backTracking(List<List<String>> result, char[][] board, int rowIndex)
    {
        if(rowIndex == board.length)
        {
            result.add(generateListFromBoard(board));
            return;
        }
        
        for(int colIndex = 0; colIndex < board.length; colIndex++)
        { 
            if(isValid(board, rowIndex, colIndex))
            {
                board[rowIndex][colIndex] = 'Q';
                backTracking(result, board, rowIndex + 1);
                board[rowIndex][colIndex] = '.';
            }
        }
    }
    
    private boolean isValid(char[][] board, int rowIndex, int colIndex)
    {
        // check if any two Qs in a line
        for(int i=0; i<rowIndex; i++)
        {
            if(board[i][colIndex] == 'Q')
                return false;
                
        }
        
        // check if any two Qs in  diagonal line
        for(int i = rowIndex - 1, j = colIndex - 1; i >= 0 && j >= 0; i--, j--)
        {
            if(board[i][j] == 'Q')
                return false;
        }
        
        for(int i = rowIndex - 1, j = colIndex + 1; i >= 0 && j < board.length; i--, j++)
        {
            if(board[i][j] == 'Q')
                return false;
        }
        
        return true;
    }
    
    private char[][] generateBoard(int n)
    {
        char[][] board = new char[n][n];
        
        for(int i=0; i<n; i++)
            Arrays.fill(board[i], '.');
        
        return board;
    }
    
    private List<String> generateListFromBoard(char[][] board)
    {
        List<String> list = new ArrayList<>();
        
        for(char[] row: board)
        {
            StringBuilder sb = new StringBuilder();
            for(char c : row)
            {
                sb. append(c);
            }
            
                    
            list.add(sb.toString());
        }
        
        return list;
    }
}
```