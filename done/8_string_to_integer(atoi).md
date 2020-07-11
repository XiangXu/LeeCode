# String to Integer (atoi) - (Medium)

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:

Only the space character ' ' is considered as whitespace character.

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. 

If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

Example 1:
```
Input: "42"
Output: 42
```

Exmaple 2:
```
Input: "-42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```

Example 3:
```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```

Example 4:
```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```

Example 5:
```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```             

## Solution

这道题感觉其实挺简单的, 就是要把所有的情况都考虑到然后将字符转换成long类型然后判断一下边界的情况.

这里后来看答案学到来一个将char快速转换成int的技巧:

```
 int a = str.charAt(-) -'0';
```
## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里n指的是所给str的长度.
* **Space Complexity: O(1)**: 这里只存储来一些变量而已.

```java
class Solution 
{
    public int myAtoi(String str) 
    {
        if(str == null || str.length() == 0)
            return 0;
        
        str = str.trim();
        if(str.length() == 0)
            return 0;
        
        char firstChar = str.charAt(0);
        int sign = 1;
        long result = 0;
        if(!Character.isDigit(firstChar))
        {
            if(firstChar == '+')
            {
                sign = 1;
            }
            else if(firstChar == '-')
            {
                sign = -1;
            }
            else
            {
                return 0;
            }
        }
        else
        {
            result = firstChar - '0';
        }
        
        for(int i=1; i<str.length(); i++)
        {
            char currChar = str.charAt(i);
            if(!Character.isDigit(currChar))
                break;
            
            result = result * 10 + currChar-'0';
            if(result > Integer.MAX_VALUE)
                return sign > 0 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        }
        
        return (int) result * sign;
    }
}
```
