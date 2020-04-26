# String to Integer (atoi)

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

## First Solution

Learned a trick 
```
 int a = str.charAt(-) -'0';
```

That's a clever trick. char's are actually of the same type / length as shorts. Now when you have a char that represents a ASCII/unicode digit (like '1'), and you subtract the smallest possible ASCII/unicode digit from it (e.g. '0'), then you'll be left with the digit's corresponding value (hence, 1)

Because char is the same as short (although, an unsigned short), you can safely cast it to an int. And the casting is always done automatically if arithmetics are involved

Reference:

https://stackoverflow.com/questions/4318263/java-subtract-0-from-char-to-get-an-int-why-does-this-work
 

Runtime: **5 ms**  
Memory: **40 MB**


```java
class Solution {
    public int myAtoi(String str) 
    {
        if(str == null)
            return 0;
        
        str = str.trim();
        if(str.length() == 0)
            return 0;
        
        long result = 0;
        int start = 0;
        int sign = 1;
        
        char firstChar = str.charAt(0);
        if(firstChar == '-')
        {
            start = 1;
            sign = -1;
        }
        else if(firstChar == '+')
        {
            start = 1;
            sign = 1;
        }
        
        for(int i=start; i<str.length(); i++)
        {
            if(!Character.isDigit(str.charAt(i)))
                break;
            
            result = result * 10 + Character.getNumericValue(str.charAt(i));

            if(result > Integer.MAX_VALUE)
                return sign > 0 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        }
        
        return (int)result * sign;
        
    }
}
```
**Time Complexity: O(N)**

**Space Complexity: O(1)**
