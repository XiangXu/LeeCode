# Reverse Integer - (Easy)

Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

```
Input: 123
Output: 321
```

Example 2:

```
Input: -123
Output: -321
```

Example 3:

```
Input: 120
Output: 21
```
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Solution

一般来说如果要倒序一个数字最好的办法就是取模10, 下面我来举个例子:

```
123 % 10 = 3
12 % 10 = 2
1 % 10  = 1

3 * 10 + 2 = 32 * 10 + 1 = 321
```


```java
class Solution 
{
    public int reverse(int x) 
    {      
        if(x >= -9 && x <= 9)
            return x;
        
        long result = 0;         
        while(x != 0)
        {
            result = result * 10 + x % 10;
            x = x / 10;  
            if(result > Integer.MAX_VALUE || result < Integer.MIN_VALUE)
                return 0;
        }
        
        return (int)result;
    }
}


```