# Integer to roman - (Medium)
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.  

Symbol       Value  
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
Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.  

Example 1:
```
Input: 3
Output: "III"
```

Example 2:
```
Input: 4
Output: "IV"
```

Example 3:
```
Input: 9
Output: "IX"
```

Example 4:
```
Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

Example 5:
```
Input: 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Solution

这道题目要求我们将数字转换成罗马字符, 其实还是挺直观的, 这道题目所给的范围是1到3999, 所以我们会有以下的情况:

在千位的情况:  String[] M = {"", "M", "MM", "MMM"};
在百位的情况:  String[] C = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
在十位的情况:  String[] X = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
在个位的情况:  String[] I = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};

接下来我们拿出所给字符串的每一位对应的来找在各位数组中对应的罗马数值:

在千位的情况: M[num/1000]
在百位的情况: C[(num%1000)/100]
在十位的情况: X[(num%100)/10]
在个位的情况: I[(num%10)]

最后我们将所有的字符串加起来的话就是最终的结果了.

## 空间时间复杂度分析:

* **Time Complexity: O(1)**: 只是做了一些计算.
* **Space Complexity: O(1)**: 只声明了一些定量的数组.

```java
class Solution
{
    public String intToRoman(int num) 
    {
        String[] M = {"", "M", "MM", "MMM"};
        String[] C = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String[] X = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String[] I = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        
        return M[num/1000] +  C[(num%1000)/100] + X[(num%100)/10] + I[(num%10)];
    }    
}
```