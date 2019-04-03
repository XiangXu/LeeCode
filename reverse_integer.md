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

If the given integer has only one digit, then we can just return it.
Use a boolean to track weather the given integer is a negative number or not.
Use a integer list to store all the numbers. 
Use %10 to get last digit. 
Use /10 to get rest digits.
 
Runtime: **20 ms**

```java
class Solution 
{
    public int reverse(int x) 
    { 
        if(x < 10 && x > -10)
            return x;
        
        boolean isMinus = false;
        List<Integer> nums = new ArrayList<>();
        
        if(x < 0)
        {
            isMinus = true;
            x = -x;
        }

        while(x > 0)
        {
            nums.add(x % 10);
            x = x / 10;
        }
        
        nums.add(x % 10);
        
        x = 0;
        for(int i=0; i<nums.size()-1; i++)
        {
            if(nums.get(i) != 0)
            {
                x += Math.pow(10, nums.size()-2-i) * nums.get(i); 
                if(x >= Integer.MAX_VALUE)
                {
                    x = 0;
                    break;
                }
            }
        }
        
        if(isMinus)
            x = -x;
        
        return x;
    }
}

```
