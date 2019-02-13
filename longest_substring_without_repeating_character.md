# Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


## First Solution

Loop all the characthers and try to apppend each character to a new String, meanwhile check if that character already exist or not.

If that character doesn't exist in that new String we just append that character and continue to loop.

If that character does exist in that new String, we remove the same old character in that string and append the new character then continue to loop.

We also save size into an size arry to track each substring's size. 
 
Runtime: **29 ms**

```java
class Solution {
    public int lengthOfLongestSubstring(String s)
    {
        int result = 0;
        
        if(s != null && s.length() > 0)
        {
            char[] cArray = s.toCharArray();          
            List<Integer> sizes = new ArrayList<>();
            String sb = cArray[0]+"";
            sizes.add(1);
            for(int i=1; i <cArray.length; i++)
            {
                int index = sb.indexOf(cArray[i]);
                
                if (index == -1)
                {
                    sb+= cArray[i]+"";
                }
                else
                {
                    String newStr = sb.substring(index+1);
                    sb = newStr+cArray[i];
                }
                
                  sizes.add(sb.length());
            }
            
            
            for(int i:  sizes)
            {
                if(result < i)
                    result = i;
            }
            
        }
        
        return result;
    }
}
```

## Second Solution

Removed results array so we don't need another loop at end. Check length each time is enougth.

Runtime: **25ms**

```java
class Solution {
    public int lengthOfLongestSubstring(String s)
    {
        int result = 0;
        
        if(s != null && s.length() > 0)
        {
            char[] cArray = s.toCharArray();          
            String sb = cArray[0]+"";;
            result = 1;
            for(int i=1; i <cArray.length; i++)
            {
                int index = sb.indexOf(cArray[i]);
                
                if (index == -1)
                {
                    sb+= cArray[i]+"";
                }
                else
                {
                    String newStr = sb.substring(index+1);
                    sb = newStr+cArray[i];
                }
                
                if(sb.length() > result)
                    result = sb.length();
            }
            
        }
        
        return result;
    }
}
```
