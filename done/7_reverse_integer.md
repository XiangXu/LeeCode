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

这里要注意一个越界的问题, **所以我们可以先用long类型来表示结果, 最后转换成int. 但是如果当前long的值超过了Integer.MAX_VALUE, 我们直接返回0**.

## 空间时间复杂度分析:

* **Time Complexity: O(log(n))**: 这里差不多是log10.
* **Space Complexity: O(1)**: 这里只存储来一些变量而已.


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