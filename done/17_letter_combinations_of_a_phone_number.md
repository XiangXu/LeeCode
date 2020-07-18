# Letter Combinations of a Phone Number

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example:  

Input: "23"  
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]

## Solution

这道题目我第一次做的时候并没有做出来, 想到的就是暴力破解法, 后来在深入的学习了算法以后, 发现其实这道题是可以用到DFS来解决的.

感觉想用文字来解释其实挺难的, 我们这里就直接列出代码, 其实看到代码以后逻辑还是比较清晰的.

这里要注意的是这段代码:

```java
//a -> ad -> a -> ae -> a -> af
//  -> b -> bd -> be -> bf.....
sb.deleteCharAt(sb.length()-1);
```

其实就是每次完成以后我们需要退一位, 然后再进行下一次append, 仔细看注释的话其实就一目了然了.

一般这种组合题的话都会在递归的方法里需要用一个for循环来拿出所有的可能性.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是指递归执行的次数其实也就是两个字母对应字符串的的长度相乘之和.
* **Space Complexity: O(n)**: 定义了一个list来存储结果, n的话为最总结果的长度.

```java
class Solution 
{
    // define keyboard, index matches the keyboard numbers
    private static final String[] keyboard = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    public List<String> letterCombinations(String digits) 
    {
        if(digits == null || digits.length() == 0)
            return Collections.emptyList();
        
        List<String> result = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        
        dfs(0, digits, sb, result);
        
        return result;
    }
    
    private void dfs(int index, String digits, StringBuilder sb, List<String> result)
    {
        if(index == digits.length())
        {
            result.add(sb.toString());
            return;
        }
        
        String letters = keyboard[digits.charAt(index)-'0'];
        for(char letter : letters.toCharArray())
        {
            sb.append(letter);
            dfs(index+1, digits, sb, result);
            //a -> ad -> a -> ae -> a -> af
            //  -> b -> bd -> be -> bf.....
            sb.deleteCharAt(sb.length()-1);
        }
    }
    
}
```

