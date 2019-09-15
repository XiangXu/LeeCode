# Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[               <br>
  "((()))",     <br>
  "(()())",     <br>
  "(())()",     <br>
  "()(())",     <br>
  "()()()"      <br>
]

## First Solution
1. We use a recursion to generate all parentheses.
2. Only add valid String into result list.

Runtime: **3 ms**

```java

class Solution {
    public List<String> generateParenthesis(int n) 
    {
        List<String> result = new ArrayList<>();
        generateAll(new char[2 * n], 0, result);
        return result;
    }
    
    private void generateAll(char[] current, int position, List<String> result)
    {
        if(position == current.length)
        {
            if(isValid(current))
                result.add(new String(current));
        }
        else
        {
            current[position] = '(';
            generateAll(current, position + 1, result);
            current[position] = ')';
            generateAll(current, position + 1, result);
        }
    }
    
    private boolean isValid(char[] current)
    {
        int balance = 0;
        for(char c: current)
        {
            if(c == '(') 
                balance ++;
            else 
                balance --;
            if(balance < 0)
                return false;
        }
        return (balance == 0);
    }
}

```

## Second Solution

Instead of adding '(' and ')' everytime, we keep track of the number of opening brackets and closing bracket. 

Runtime: 1 ms

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
