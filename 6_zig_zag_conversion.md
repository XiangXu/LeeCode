# ZigZag Conversion

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

P     I    N
A   L S  I G
Y A   H R
P     I

## First Solution

Declare an StringBuilder array to store character in zigzag pattern.

Runtime: **4 ms**  
Memory: **39.6 MB**

```java
 class Solution 
{
    public String convert(String s, int numRows) 
    {
        if(numRows == 1)
            return s;
        
        StringBuilder[] sbArray = new StringBuilder[numRows];
        for(int i=0; i < numRows; i++)
        {
            sbArray[i] = new StringBuilder();
        }
        
        int currentRow = 0;
        boolean directionChange = false;
        
        for(char c: s.toCharArray())
        {
            sbArray[currentRow].append(c);
            if(currentRow == 0 || currentRow == numRows -1)
                directionChange = !directionChange;
            
            currentRow += directionChange ? 1 : -1;
        }
        
        for(int i=1; i<sbArray.length; i++)
        {
            sbArray[0].append(sbArray[i]);
        }
        
        return sbArray[0].toString();
    }
}

```

**Time Complexity: O(N)**

**Space Complexity: O(N)**

StringBuilder
