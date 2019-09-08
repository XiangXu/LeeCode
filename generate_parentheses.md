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
