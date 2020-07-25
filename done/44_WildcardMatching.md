# Wildcard Matching

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*'.

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
```

The matching should cover the entire input string (not partial).

Note:

* s could be empty and contains only lowercase letters a-z.
* p could be empty and contains only lowercase letters a-z, and characters like ? or *

Example 1

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

Example 2

```
Input:
s = "aa"
p = "*"
Output: true
Explanation: '*' matches any sequence.
```

Example 3

```
Input:
s = "cb"
p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

Example 4:

```
Input:
s = "adceb"
p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

Example 5:

```
Input:
s = "acdcb"
p = "a*c?b"
Output: false
```

# Solution

这道题我开始以为自己能过做出来, 尝试提交了5次以后发现corner case实在是太多了, 看了答案发现和我一样用了双指针, 但是答案的的写法简洁太多了.

下面我们通过一个test case来分析:

```
a c d c c d
* c d
```
    
这道题其实大体的思路就是声明两个指针分别指向s和p的第一位字符, 如果两个字符相同或者p所指的字符是'?', 同时向右移动字符. 但是当p所指的字符为'*'的时候, 我们就需要注意了.

\*使得我们可以在s中跳过一些字符串, 那么*的下一位就尤其的重要了, 因为它是来决定结果符不符合条件的. 

所给的test case 可以看出, p中*的下一位是c, c在字符串s中出现了三次, 分别在index 1, 3, 4这三个位置. 我们需要依次尝试.
    
1. index = 1的时候, 下一位d = d, 满足条件, 但是再向右移动的时候, p的指针已经越界了但是s的指针指向的是c, 说明index=1不满足条件.
2. index = 3的时候, 下一位是c != d, 说明index=3不满足条件.
3. index = 4的时候, 下一位是 d = d, 满足条件, 与此同时, p和s的指针都已经指向了最后一位, 满足条件, 所以结果为true.
    
理解了上面的思想以后, 我们就知道了我们需要记录p中*的位置, 还需要记录s中上一次和p字符串match的位置, 在条件不满足的时候将s中的指针返回到上一个match的位置.

## 空间时间复杂度分析:

* **Time Complexity: O(m+n)**: 我们遍历两个字符串中的字符, 所以m+n为两个字符串长度相加的和.
* **Space Complexity: O(1)**: 只声明了一些变量.

```java
class Solution 
{    
    public boolean isMatch(String s, String p) 
    {
        int sPointer = 0;
        int pPointer = 0;
        
        int sLen = s.length();
        int pLen = p.length();
        
        // previous matched char index in s
        int preMatchIndex = -1;
        int preStarIndex = -1;
        
        while(sPointer < sLen)
        {
            if(pPointer < pLen && (s.charAt(sPointer) == p.charAt(pPointer) || p.charAt(pPointer) == '?'))
            {
                sPointer ++;
                pPointer ++;
            }
            else if(pPointer < pLen && p.charAt(pPointer) == '*')
            {
                preStarIndex = pPointer;
                pPointer ++;
                preMatchIndex = sPointer;
            }
            else if(preStarIndex != -1)
            {
                pPointer = preStarIndex + 1;
                preMatchIndex ++;
                sPointer = preMatchIndex;
            }
            else
                return false;
        }
        
        //aa and aa*
        //abc and abcd
        while (pPointer < p.length() && p.charAt(pPointer) == '*')
            pPointer++;
        
        return pPointer == p.length();
        
    }
}
```