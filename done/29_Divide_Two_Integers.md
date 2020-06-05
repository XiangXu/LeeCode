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

## First Solution

Runtime: **1 ms**

Memory: **36.7 MB**

```java
class Solution 
{
    public int divide(int dividend, int divisor) 
    {
        int sign = 1;
        if((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0))
            sign = -1;
        
        long ldividend = Math.abs((long)dividend);
        long ldivisor = Math.abs((long)divisor);
        
        if (ldivisor == 0) 
            return Integer.MAX_VALUE;
        if(ldividend < ldivisor || ldividend == 0)
            return 0;
        
        long lresult = ldivide(ldividend, ldivisor);
        
        int result;
        if(lresult > Integer.MAX_VALUE)
            result = sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        else
            result = sign * (int)lresult;

        return result; 
            
    }
    
    private long ldivide(long ldividend, long ldivisor)
    {
        if (ldividend < ldivisor) 
            return 0;
        
        long sum = ldivisor;
        long multiple = 1;
        while ((sum+sum) <= ldividend) 
        {
            sum += sum;
            multiple += multiple;
        }

        return multiple + ldivide(ldividend - sum, ldivisor);
    }
}
```

**Time Complexity: O(logN)** 

**Space Complexity: O(logN))**