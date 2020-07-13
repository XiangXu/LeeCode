# Roman to integer - (Easy)

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.  

Symbol       Value.   
I             1   
V             5  
X             10   
L             50   
C             100   
D             500   
M             1000   
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.  

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:  

I can be placed before V (5) and X (10) to make 4 and 9.   
X can be placed before L (50) and C (100) to make 40 and 90.   
C can be placed before D (500) and M (1000) to make 400 and 900.  
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.  

Example 1:
```
Input: "III"   
Output: 3.  
```

Example 2:  
```
Input: "IV"   
Output: 4   
```

Example 3:   
```
Input: "IX"  
Output: 9  
```

Example 4:  
```
Input: "LVIII"  
Output: 58  
Explanation: L = 50, V= 5, III = 3  
```

Example 5:  
```
Input: "MCMXCIV"  
Output: 1994  
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Solution

这道题目其实是上一道题目的反转, 解法其实还是挺直观的. 首先我们需要一个如下的方法来将字符转换成数字:

```java
private int convertCharToInt(char c)
{
    switch(c)
    {
        case 'I': return 1;
        case 'V': return 5;
        case 'X': return 10;
        case 'L': return 50;
        case 'C': return 100;
        case 'D': return 500;
        case 'M': return 1000;
    }
    
    return 0;
}
```

接下来我们需要考虑一个情况, 我们拿"MCM"当一个例子:

1. 根据第一个字符'M', 我们可以得到: result = 1000;
2. 根据第二个字符'C', 我们可以得到: result = 1000 + 100 = 1100;
3. 根据第三个字符'M', 这个时候M的值是要比之前的那个C大的, 这个时候我们就需要: result = (1100 - 100) + (1000 - 100) = 1900

一旦我们理解了上面的计算方式, 那么这道题就非常的简单了. 罗马数字其实要注意的规律就是当后面的字符串比前面大的时候需要处理一下.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是指所给字符串的长度, 因为这里我们遍历了这个字符串.
* **Space Complexity: O(1)**: 只声明了一些定量的数组.

```java
class Solution 
{
    public int romanToInt(String s) 
    {
        if(s == null || s.length() == 0)
            return 0;
        
        int result = convertCharToInt(s.charAt(0));
        
        for(int i=1; i<s.length(); i++)
        {
            int pre = convertCharToInt(s.charAt(i-1));
            int curr = convertCharToInt(s.charAt(i));
            
            if(curr > pre)
            {
                result = result - pre + (curr - pre);
            }
            else
            {
                result += curr;
            }
        }
        
        return result;
    }
    
    
    private int convertCharToInt(char c)
    {
        switch(c)
        {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
        }
        
        return 0;
    }
}
```