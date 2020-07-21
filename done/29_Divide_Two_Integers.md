# Divide Two Integers

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero, which means losing its fractional part. For example, truncate(8.345) = 8 and truncate(-2.7335) = -2.

Example 1: 

```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = truncate(3.33333..) = 3.
```

Example 2:

```
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = truncate(-2.33333..) = -2.
```

## Solution

首先这道题描述中说明我们要考虑int overflow的问题, 那么我们肯定要使用long来做了. 由于dividend和divisor都有可能为正数或者负数, 我们可以用一个sign来记录正负数情况, 然后将两个值都变为正数进行操作, 这样简化了逻辑. 接下来我们考虑以下临界情况:
1. 这里我测试了leetcode的testcase, 当divisor为0的时候会报错, 所以我们可以忽略这个.
2. 如果dividend < divisor的话, 返回0.
3. 如果dividend = divisor的话, 返回1.

考虑完了临界情况, 我们来看一下正常解题的思路: 

我第一个想到的是如果我们用count记录每一次dividend - divisor知道dividend < = 0, 那么这个count就是最终的答案. 这个方法理论上是可行的, 但是最终我得到来Time Limit Exceeded, 这个是可以预料到的, 这里就不实现代码了. 

看了答案以后我发现了一种思路, 我们用一个具体的例子来看, dividend = 10, divisor = 3.

1. 我们假设sum = diviosr = 3, multiple = 1, 那么如果sum + sum = 6 < 10, 那么我们更新sum += sum = 6, multiple += multiple = 2.
2. 我们继续上面的操作: sum + sum = 12 > 10, 那么此时sum = 6, multiple = 2, 此时余数为10 - 6 = 4. 
3. 我们再用同样的方法计算4能得到multiple = 1, 所以最终的结果就为2 + 1 = 3.

## 空间时间复杂度分析:

* **Time Complexity: O(logN)**: 这里while循环中sum+sum采用了类似二分法的做法.
* **Space Complexity: O(logN))**: 这里用了递归的方法来计算result.

```java
class Solution 
{
    public int divide(int dividend, int divisor) 
    {
        boolean isNegative = ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0));
        
        long dividendLong = Math.abs((long)dividend);
        long divisorLong = Math.abs((long)divisor);
        
        if(dividendLong < divisorLong)
            return 0;
        
        if(dividendLong == divisorLong)
            return isNegative ? -1 : 1;
        
        long result = dividHelper(dividendLong, divisorLong);
        
        if(result > Integer.MAX_VALUE)
            return isNegative ? Integer.MIN_VALUE : Integer.MAX_VALUE;
        
        return isNegative ? -(int)result : (int)result;
    }
    
    
    private long dividHelper(long dividend, long divisor)
    {
        if(dividend < divisor)
            return 0;
        
        long sum = divisor;
        long multiple = 1;
        
        while(sum + sum <= dividend)
        {
            sum += sum;
            multiple += multiple;
        }
        
        return multiple + dividHelper(dividend - sum, divisor);
    }
}
```








