# Implement strStr()

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

Example 2:

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

## Solution

这道题目感觉其实还是挺简单的, 用一个substring就能够解决, 这里就不再过多说明了, 代码应该一目了然.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 遍历haystack字符串, n应该为haystack.length() - needle.length().
* **Space Complexity: O(1)**: 这里没有声明任何东西.


```java
class Solution 
{
    public int strStr(String haystack, String needle) 
    {
        if(needle == null || needle.length() == 0)
            return 0;
        
        for(int i=0; i<=haystack.length() - needle.length(); i++)
        {
            if(haystack.substring(i, i+needle.length()).equals(needle))
                return i;
        }
        
        return -1;
    }
}
```