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
class Solution {
    public List<String> generateParenthesis(int n) 
    {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }
    
    public void backtrack(List<String> result, String currentStr, int open, int close, int max)
    {
        if(currentStr.length() == max * 2)
        {
            result.add(currentStr);
            return;
        }
        
        if(open < max)
            backtrack(result, currentStr+"(", open+1, close, max);
        
        if(close < open)
            backtrack(result, currentStr+")", open, close+1, max);
    }
}
```

**Time Complexity: O(n<sup>2</sup>)** 

**Space Complexity: O(n)**