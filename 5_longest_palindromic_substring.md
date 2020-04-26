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
    public String longestPalindrome(String s) 
    {
        if(s == null || s.length() == 0)
            return "";
        
        int start = 0, end = 0;
        
        for(int i=0; i<s.length(); i++)
        {
            int len1 = expendFromCenter(s, i, i);
            int len2 = expendFromCenter(s, i, i+1);
            
            int len = Math.max(len1, len2);
            
            // i = 2, start = 1, end = 3, len = 3
            // i = 1, start = 1, end = 2, len = 2
            
            if(len > end - start)
            {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
      
        return s.substring(start, end + 1);
    }
    
    private int expendFromCenter(String s,int left, int right)
    {
        String current = "";
        while(left >=0 && right < s.length() && s.charAt(left) == s.charAt(right))
        {   
            left --;
            right ++;
        }
        
        return right - left - 1;
    }

}
```

**Time Complexity: O($n^2$)**

**Space Complexity: O(1)**





