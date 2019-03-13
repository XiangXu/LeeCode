# Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
Follow up:

Coud you solve it without converting the integer to a string?

## First Solution

1. If the given integer is less than 0, it will always return false.
2. If the give integer is >=0 and less than 10, it will alwasy return true.
3. Reverse integer by using /10 and %10
 
Runtime: **69 ms**

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0)
            return false;
        else if(x >= 0 && x < 10)
            return true;
        
        int reverseInt = getReverseInt(x);
        
        if(x == reverseInt)
            return true;
        else 
            return false;
    }
    
     private int getReverseInt(int value) 
    {
        int resultNumber = 0;
        for (int i = value; i !=0; i /= 10) 
        {
            resultNumber = resultNumber * 10 + i % 10;
        }
        return resultNumber;        
    }
    

}
```
