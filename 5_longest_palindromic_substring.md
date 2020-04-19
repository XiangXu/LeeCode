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
dp we try to cover all cases.

Take "b a b a d" as an example

if i = 0 -> b
   j = 4 -> d
   
if i = 1 -> a
   j = 3 -> a
   
if i = 2 -> b
   j = 2 -> b
   
if i = 2 -> b
   j = 3 -> a
   
   2 + 1 = 3 -> a
   3 - 1 = 2 -> b this doesn't make sense
 
Runtime: **215 ms**  
Memory: **66 MB**

```java
class Solution 
{
    public String longestPalindrome(String s) 
    {
        if(s == null || s.length() == 0)
            return s;
        
        String result = "";
        int max = 0;
        
        boolean[][] dp = new boolean[s.length()][s.length()];
        
        for(int i=0; i<s.length(); i++)
        {
            for(int j=0; j<=i; j++)
            {
                dp[j][i] = s.charAt(j) == s.charAt(i)  && ((i - j <= 2) || dp[j+1][i-1]);
                if(dp[j][i])
                {
                    if(i - j + 1 > max)
                    {
                        max = i - j + 1;
                        result = s.substring(j, i+1);
                    }
                }
            }
        }
        
        return result;
    
    }
}
```
**Time Complexity: O($n^2$)**

**Space Complexity: O($n^2$)**

## Second Solution

Two example: 
"b a b a d"     start from center "b"
"b a b a d a"   start from center "b a"
1. a b a left = 1, right = 2; 
2. b a b a left =0, right 3, doesn't match palindromic substring

Runtime: **657 ms**  
Memory: **485.3 MB**

```java
class Solution 
{
    private String result = "";
    
    public String longestPalindrome(String s) 
    {
        if(s == null || s.length() == 0)
            return s;
        
        for(int i=0; i<s.length(); i++)
        {
            expendAroundCenter(s, i, i);
            expendAroundCenter(s, i, i+1);
        }
        
        return result;
    }
    
    public void expendAroundCenter(String s, int left, int right)
    {
        String current = "";
        while(left >=0 && right < s.length() && s.charAt(left) == s.charAt(right))
        {            
            current = s.substring(left, right+1);   
            if(current.length() > result.length())
                result = current;
            
            left --;
            right ++;   
        }    
    }
    
}
```

**Time Complexity: O($n^2$)**

**Space Complexity: O(n)**





