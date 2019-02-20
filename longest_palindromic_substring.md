# Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

## First Solution
Iterate all characters in that String 
 
Runtime: **2633 ms ms**

```java
class Solution 
{
    public String longestPalindrome(String s) 
    {
        String result = "";
        
        if(s != null && s.length() > 0)
        {
            for(int i=0; i<s.length(); i++)
            {
                for(int j=i+1; j<=s.length(); j++)
                {
                    String tempStr = s.substring(i, j);
                    if(isPalindromicString(tempStr) && result.length() < tempStr.length()) 
                    {
                        result = tempStr;
                    }
                }
            }
        }
        
        return result;
    }
    
    private boolean isPalindromicString(String s)
    {
        boolean result = false;
        if(s != null && s.length() > 0)
        {
            int left = 0;
            int right = s.length() - 1;
            
            while(left < right)
            {
                if(s.charAt(left) != s.charAt(right))
                {
                    return false;
                }

                left++;
                right--;
            }
        }
        return true;
    }
}
```
