# Longest Substring Without Repeating Characters - (Medium)

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

## Solution

这道题目是一个典型的滑动窗口的问题, 具体步骤如下:

1. 首先我们需要用一个HashMap来存储每次遍历的字符和index的位置, 这样的好处是我们可以跳过一些重复字符.
2. 假设我们有两个指针A和B开始都在index等于0的位置, 然后我们向后移动指针B.
3. 如果指针B当前字符不在HashMap里的话, 将当前字符和index存入HashMap.
4. 如果指针B当前字符在HashMap的话，说明有重复的字符。这时候从HashMap中拿到重复字符的index, 然后将A = index+1.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 遍历字符串S所需要的时间.
* **Space Complexity: O(min(m, n))**: 我们需要O(k)来存储不重复的字符, m表示字符串s的长度而n表示字母表的上限.


```java
class Solution 
{
    public int lengthOfLongestSubstring(String s) 
    {
        if(s == null || s.length() == 0)
            return 0;
        
        Map<Character, Integer> map = new HashMap<>();

        int result = 0;
        int i=0;
        
        for(int j=0; j<s.length(); j++)
        {
            char currChar = s.charAt(j);
            if(map.containsKey(currChar))
                i = Math.max(i, map.get(currChar) + 1);
            
            map.put(currChar, j);
            result = Math.max(j-i+1, result);
        }
        
        return result;
    }
}
```
