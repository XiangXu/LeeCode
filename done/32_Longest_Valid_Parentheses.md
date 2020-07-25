# Longest Valid Parentheses


Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example 1:

```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

Example 2:

```
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()
```

## Solution

这道题感觉和20题类似, 看到这类题目第一反应就是要用stack. 具体的思路是我们看到'('就放入stack, 看到')'就从stack中那最上面的出来. 但是相比20题, 这道题的难点在于要找到最长的valid parenthese. 我开始没有想到很好的方法, 借鉴来20题的思路, 实现了一种暴力破解的方法, 但是果不其然TLE超时了.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>3</sup>)**: 这里我们有3个for循环来遍历s.
* **Space Complexity: O(n)**: 这里我们只声明了一个stack来判断结果.

```java
class Solution 
{
    public int longestValidParentheses(String s) 
    {
        if(s == null || s.length() == 0)
            return 0;
        
        int longtestLen = 0;
        
        for(int i=0; i<s.length(); i++)
        {
            for(int j=i+2; j<=s.length(); j+=2)
            {
                if(isValid(s.substring(i, j)))
                {
                    longtestLen = Math.max(j-i, longtestLen);
                }
            }
        }
        
        return longtestLen;
    }
    
    private boolean isValid(String s)
    {
        Stack<Character> stack = new Stack<>();
        
        for(char c : s.toCharArray())
        {
            if(c == '(')
                stack.push(c);
            else if(stack.isEmpty())
                return false;
            else 
                stack.pop();
        }
        
        return stack.isEmpty();
    }
}
```

看了答案以后, 有一种解法也是用stack解决的, 大概思路是存储index在stack中, 但是我觉得如果真的在面试中很难想到, 因为具体的实现方式太精妙了. 另一中答案Without extra space感觉更容易理解, 我们想一下怎么才能够构成valid parentheses. 其实就是'('和')'的数量相等. 那么如果我们定义两个变量初始化为0, 然后我们分别从左往右遍历s, 发现'('的时候right++, 发现'0'的时候left++, **那么当left == right的时候说明当前是一个valid parentheses. 如果right > left则说明当前肯定不符合结果, 这时候把left和right清0继续知道遍历完s**. 如果test case是"())"的话我们的答案肯定是正确的. 但是如果test case是"(()"的话此时,left = 2, right =1, 我们最后的结果会返回0, 因为永远不会达到left == right, 那么我们怎么解决这个问题呢, 很简单, 我们再从右到左遍历s就可以了! 

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 我们循环了两次s, n为s的长度.
* **Space Complexity: O(1)**: 我们这里只声明了一些变量.

```java
class Solution 
{
    public int longestValidParentheses(String s) 
    {
        if(s == null || s.length() <= 1)
            return 0;
        
        int result = 0;
        int left = 0;
        int right = 0;
        
        //traverse s from left to right to handle s like "())".
        for(int i=0; i<s.length(); i++)
        {
            if(s.charAt(i) == '(') 
                left++ ;
            else 
                right++;
            
            if(left == right)
                result = Math.max(result, left + right);
            else if(right > left)
            {
                left = 0;
                right = 0;
            }
        }
        
        // reset counters
        left = 0;
        right = 0;
        
        //traverse s from right to left to handle s like "(()".
        for(int i=s.length()-1; i>=0; i--)
        {
            if(s.charAt(i) == ')') 
                right++ ;
            else 
                left++;
            
            if(right == left)
                result = Math.max(result, left + right);
            else if(left > right)
            {
                left = 0;
                right = 0;
            }
        }
        
        return result;
    }
}
```
    
        