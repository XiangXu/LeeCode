# Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:

Input: ["flower","flow","flight"]<br>  
Output: "fl"<br>
<br>

Example 2:

Input: ["dog","racecar","car"]<br>
Output: ""<br>
Explanation: There is no common prefix among the input strings.

Note:

All given inputs are in lowercase letters a-z.


## First Solution
1. Find the shortest String in given array first. 
2. Compare each charachters in Shortest String with Strings in array to see if they are match or not.

Runtime: **1 m**

```java

class Solution 
{
    public String longestCommonPrefix(String[] strs) 
    {
        StringBuilder sb = new StringBuilder();
        
        if(strs.length > 0)
        {
            String shortestStr = strs[0];
            
            for(int i=1; i<strs.length; i++)
            {
                if(strs[i].length() < shortestStr.length())
                {
                    shortestStr = strs[i];
                }
            }
            
            boolean isCommon = true;
            char[] shortestChars = shortestStr.toCharArray();
            
            for(int i=0; i<shortestChars.length; i++)
            {
                char currentChar = shortestChars[i];
               
                for(int j=0; j<strs.length; j++)
                {
                    char tempChar = strs[j].toCharArray()[i];

                    if(currentChar != tempChar){
                        isCommon = false;
                        break;
                    }
                        
                }
                
                if(isCommon)
                    sb.append(currentChar);
                else
                    break;
                
            }
            
            return sb.toString();
        }
            
        
        return "";
    }
}
```
