# Rotate Image

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

Example 2:

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

## Solution

这道题我开始的想法是直接将Matrix从下到上, 从左到右遍历, 依次替换. 但是我发现这样是行不通的.
```
[1,2,3]
[4,5,6]
[7,8,9]
```

比如说我们从7开始向上遍历, 这时候用7把1替换掉此时为
```
[7,2,3]
[4,5,6]
[7,8,9]
```
这样我们就丢失了1, 答案肯定是不对的. 看了下答案找思路才发现我把这道题想的太简单了, 这里我们并不能一口吃成一个胖子.具体的解法分为两个部分:

Matrix一定是正方形!

假设我们所给的matrix为:
```
[1,2,3]
[4,5,6]
[7,8,9]
```

那么第一步我们先将matrix竖直排序:
```
[1,4,7]
[2,5,8]
[3,6,9]
```

接下来我们再将matrix倒着排序:
```
[7,4,1]
[8,5,2]
[9,6,3]
```

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 遍历Matrix的两个for循环.
* **Space Complexity: O(1)**: 只定义了一些变量.

```java
class Solution 
{   
    public void rotate(int[][] matrix) 
    {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return;
        
        // Update matrix from top to bottom and left to right.
        for(int i=0; i<matrix.length; i++)
        {
            for(int j=i; j<matrix[0].length; j++)
            {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
        
        // Reverse matrix
        for(int i=0; i<matrix.length; i++)
        {
            for(int j=0; j<matrix.length/2; j++)
            {
                int swapIndex = matrix.length-1-j;
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[i][swapIndex];
                matrix[i][swapIndex] = tmp;
            }
        }
    }
}
```