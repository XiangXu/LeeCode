# Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  
Note that an empty string is also considered valid.  

Example 1:  

```
Input: "()"
Output: true
```
Example 2:

```
Input: "()[]{}"
Output: true
```

Example 3:

```
Input: "(]"
Output: false
```

Example 4:

```
Input: "([)]"
Output: false
```

Example 5:

```
Input: "{[]}"
Output: true
```

## Solution

这道题就是典型的配对题目, 第一次看到这道题的时候, 没什么经验感觉挺棘手的. 一般这种题目我们肯定需要用到stack的特性来做, 一旦了解这个其实这道题目就挺简单了.


## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里我们遍历了所给的String s, s.
* **Space Complexity: O(n)**: 这里我们只声明了一个stack.


```java
class Solution 
{
    public boolean isValid(String s) 
    {
        if(s == null || s.length() == 1 || s.length() % 2 != 0)
            return false;
        
        if(s.length() == 0)
            return true;
        
        Stack<Character> stack = new Stack<>();
        
        for(char c : s.toCharArray())
        {
            if(c == '(')
                stack.push(')');
            else if(c == '{')
                stack.push('}');
            else if(c == '[')
                stack.push(']');
            else
            {
                if(stack.isEmpty() || c != stack.pop())
                    return false;
            }
        }
        
        return stack.isEmpty();
    }
}
```
