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

Runtime: **0 ms**

Memory: **37.3 MB**

```java
class Solution 
{
    public String longestCommonPrefix(String[] strs) 
    {        
        if(strs == null || strs.length == 0)
            return "";
        
        String result = strs[0];
        for(int i=1; i<strs.length; i++)
        {
            while(strs[i].indexOf(result) != 0)
            {
                result = result.substring(0, result.length() - 1);
            }
        }
        
        return result;
    }
}
```

**Time Complexity: O(n)**

**Space Complexity: O(n*l)**

length of str[0]
