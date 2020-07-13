# Longest Common Prefix - (Easy)

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: ["flower","flow","flight"] 
Output: "fl"
```

Example 2:
```
Input: ["dog","racecar","car"]
Output: "
Explanation: There is no common prefix among the input strings.
```

Note:

All given inputs are in lowercase letters a-z.


## Solution

这道题还是比较简单的. 我的思路主要是先将所给的数组按照从小到大的顺序排序, 因为最长common prefix的话肯定是从长度最小的字符串中得来的.

然后我讲剩下的字符串用startsWith()方法依次比较这个最小的字符串, 慢慢的从右到左缩小最小字符串的长度, 最终可以得到结果. 具体实现如下:

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 这里我们遍历最小字符串中的每个字符同时遍历比较strs中剩余的字符串.
* **Space Complexity: O(1)**: 只声明了一些变量.


```java
class Solution 
{
    public String longestCommonPrefix(String[] strs) 
    {
        if(strs == null || strs.length == 0)
            return "";
        
        Arrays.sort(strs, (str1, str2) -> str1.length()-str2.length());
        
        for(int i=strs[0].length(); i>0; i--)
        {
            String subStr = strs[0].substring(0, i);
            boolean allMatch = true;
            
            for(int j=1; j<strs.length; j++)
            {
                if(!strs[j].startsWith(subStr))
                {
                    allMatch = false;
                    break;
                }
            }
            
            if(allMatch)
                return subStr;
        }
        
        
        return "";
    }
}
```


