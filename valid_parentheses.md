# Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  
Note that an empty string is also considered valid.  

Example 1:  
Input: "()"<br>
Output: true

Example 2:<br>
Input: "()[]{}"<br>
Output: true

Example 3:<br>
Input: "(]"<br>
Output: false

Example 4:<br>
Input: "([)]"<br>
Output: false<br>

Example 5:<br>
Input: "{[]}"<br>
Output: true


## First Solution
I didn't think about to use a stack until I had a look at solution.

Runtime: **1 ms**

```java

class Solution 
{
    public boolean isValid(String s) 
    {   
        Stack<Character> stack = new Stack();
        
        for(char c: s.toCharArray())
        {
            if('(' == c)
                stack.push(')');
            else if('{' == c)
                stack.push('}');
            else if('[' == c)
                stack.push(']');
            else if(stack.isEmpty() || stack.pop() != c)
                return false;
        }
        return stack.isEmpty();
    }
}
```
