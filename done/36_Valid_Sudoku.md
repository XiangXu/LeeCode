# Valid Sudoku - (Medium)`

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

Example 1

```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

Example 2:

```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

Note:

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.
* The given board contain only digits 1-9 and the character '.'.
* The given board size is always 9x9.

## Solution

这道题目我开始理解错题意导致没有做出来, 这里也要和自己再说一下一定要仔细看题. 题目是要求我们验证当前的数独是否成立, 有三个地方需要验证.

1. 每个横排中每个数字只能出现一次.
2. 每个竖排中每个数字只能出现一次.
3. 3*3的小格当中每个数字只能出现一次.

首先如果我们看到题目需要保证数字只出现一次, 那么我们肯定是需要使用的Set. 在做这道题目之前, 我一般的做法是如下
```java
if(!set.contains(val))
    set.add(val);
```
但是其实set.add(val)的方法返回类型就是boolean, 如果set中已经存在了当前的val值, 那么这个add的方法就会直接的返回false. 这个是我之前不知道的, 学习了!

这道题目另外的一个难点是如何得到3*3的row和column的index, 我们需要确保每一个sub box的数字没有重复, 具体计算如下:
```
int subRow = 3 * (i / 3) + j / 3;
int subCol = 3 * (i % 3) + j % 3;

其实3 * (i/3) 和 3*(i % 3) 是计算sub box的起始点的row和column:

(0, 0), (0, 3), (0, 6)
(3, 0), (3, 3), (3, 6)
(6, 0), (6, 3), (6, 6)

```

这样的话就会从左到右从上到下遍历sub box中的每一个数.


## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 我们遍历这个二维数组所需要的两个for循环.
* **Space Complexity: O(n)**: 我们所用的三个Set中最长的那一个.

```java
class Solution 
{
    public boolean isValidSudoku(char[][] board) 
    {
        if(board == null || board.length != 9 || board[0].length != 9)
            return false;
        
        for(int i=0; i<board.length; i++)
        {
            Set<Character> rowSet = new HashSet<>();
            Set<Character> colSet = new HashSet<>();
            Set<Character> subSet = new HashSet<>();
            
            for(int j=0; j<board[0].length; j++)
            {
                //check column duplicate
                if(board[i][j] != '.' && !colSet.add(board[i][j]))
                    return false;
                
                //check row duplicate
                if(board[j][i] != '.' && !rowSet.add(board[j][i]))
                    return false;
                
                // check if sub box contains duplicate
                int subRow = 3 * (i / 3) + j / 3;
                int subCol = 3 * (i % 3) + j % 3;
                
                if(board[subRow][subCol] != '.' && !subSet.add(board[subRow][subCol]))
                    return false;
            }
        }
        
        return true;
    }
}
```




