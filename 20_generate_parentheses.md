# Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

```
[               
  "((()))",     
  "(()())",     
  "(())()",     
  "()(())",     
  "()()()"      
]
```

## First Solution

Runtime: **1 ms**

Memory: **37.7 MB**

```java
class Solution 
{
    public boolean isValid(String s) 
    {   
        if(s == null || s.length() % 2 != 0)
            return false;
        
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

**Time Complexity: O(n)** 

**Space Complexity: O(n)**