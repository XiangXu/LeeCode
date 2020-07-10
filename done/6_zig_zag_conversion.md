# ZigZag Conversion - (Medium)

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);

Example 1:

Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"

Example 2:

Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"

Explanation:

```
P     I    N
A   L S  I G
Y A   H R
P     I
```

## Solution

这道题的解法其实挺直接的, 我们根据numRows的数量来创建相同数量的StringBuilder数组, 然后我们还需要一个boolea来决定是否需要变化顺序, 最后我们遍历字符串.

当我在写代码的时候changeDirection = !changeDirection不知道为什么我没有想到!

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里遍历字符串和初始化StringBuilder数组都需要n的时间.
* **Space Complexity: O(n)**: 这里我们用了一个StringBuilder的数组来存储结果.

```java
class Solution 
{
    public String convert(String s, int numRows) 
    {
        if(s == null || s.length() == 0 || numRows <= 0)
            return s;
        
        if(numRows == 1)
            return s;
        
        StringBuilder[] sb = new StringBuilder[numRows];
        for(int i=0; i<numRows; i++)
            sb[i] = new StringBuilder();
        
        int index = 0;
        boolean changeDirection = false;
        for(int i=0; i<s.length(); i++)
        { 
            sb[index].append(s.charAt(i));
            if(index == 0 || index == numRows-1)
                changeDirection = !changeDirection;
            
            index += changeDirection ? 1 : -1;
        }
        
        for(int i=1; i<sb.length; i++)
            sb[0].append(sb[i].toString());
        
        return sb[0].toString();
    }
}
```
