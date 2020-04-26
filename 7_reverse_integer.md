# Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

Example 1:
Input: 123
Output: 321

Example 2:
Input: -123
Output: -321

Example 3:
Input: 120
Output: 21
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## First Solution
Use long to handle integer overflow.

Runtime: **1 ms**  
Memory: **36.6 MB**

```java
class Solution {
    public int reverse(int x) 
    {
        if(x < 10 && x > -10)
            return x;
        
        long result = 0;
        while(x != 0)
        {
            result *= 10;
            result += x % 10;
            x = x / 10;
        }
        
        return (int)result == result ? (int)result : 0;
    }
}
```

**Time Complexity: O(N)**

**Space Complexity: O(1)**
