# Longest Palindromic Substring - (medium)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

## Solution

这道题目要求我们找到所给字符串中最长的回文, 那么什么是回文呢?

我们可以这样来想, 回文就是从中间的那个字符串开始, 分别向左右两边遍历, 如果左边和右边的字符串都相等的话, 那么这个字符串就是回文. 

其实这就是解决这道题目的思路, 中心扩散法.

当然这里我们需要注意的是回文会有两种不同的格式:

1. ccddaaddcc
2. ccddaddcc

我们需要考虑以上的这两种情况.

下面说一下具体的解体思路:

1. 首先我们需要一个方法expendFromCenter(int left, int right, String s), left和right其实就是回文的中心点, 由于我们知道回文存在两种不同的格式 所以需要考虑i和i+1的情况.
2. 遍历所给字符, 将当前的index传给这个方法, 得到当前字符串返回的最长回文.
3. 比较结果, 返回最长的回文.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 遍历字符串需要花费n的时间,expendFromCenter方法也需要n的时间.
* **Space Complexity: O(1)**: 我们只用了一些变量来存储结果.

```java
class Solution 
{
    public String longestPalindrome(String s) 
    {
        if(s == null || s.length() == 0)
            return s;
        
        String result = "";
        for(int i=0; i<s.length(); i++)
        {
            String str1 = expendFromCenter(i, i, s);
            String str2 = expendFromCenter(i, i+1, s);
            String str = str1.length() >= str2.length() ? str1 : str2;
            result = str.length() > result.length() ? str : result;
        }
    
        return result;
    }
    
    private String expendFromCenter(int left, int right, String s)
    {
        String str = "";
        while(left >= 0 && right <= s.length()-1 && s.charAt(left) == s.charAt(right))
        {
            str = s.substring(left, right+1);
            left --;
            right ++;
        }
        
        return str;
    }
}
```
   



