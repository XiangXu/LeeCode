# Count and Say

The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

Note: Each term of the sequence of integers will be represented as a string.

Example 1:

```
Input: 1
Output: "1"
Explanation: This is the base case.
```

Example 2:

```
Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
```

## Solution

这道题感觉其实题目有点难弄懂, 我也是去谷歌了别人对这道题目的解释才弄懂的, 题目的意思其实是这样:

1.     1
2.     11
3.     21
4.     1211
5.     111221

2的话其实是对1的解释, 就是有一个一, 所以是11.

3的话其实是对2的解释, 就是有两个一, 所以是21.

4的话其实是对3的解释, 就是有一个二和一个以一, 所以是1211

这道题感觉也没有什么规律, 就是暴力破解.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 遍历数字n和字符串的两个for循环.
* **Space Complexity: O(1)**: 只定义了一些变量.

```java
class Solution 
{
    public String countAndSay(int n) 
    {
        String str = "1";
        
        // how many times we count
        for(int i=1; i<n; i++)
        {
            StringBuilder sb = new StringBuilder();
            char firstChar = str.charAt(0);
            int count = 0;
            
            //generate new String based on previous String
            for(int j=0; j<=str.length(); j++)
            {
                if(j == str.length())
                {
                    sb.append(count).append(firstChar);
                    break;
                }
                
                if(firstChar == str.charAt(j))
                {
                    count ++;
                }
                else
                {
                    sb.append(count).append(firstChar);
                    firstChar = str.charAt(j);
                    count = 1;
                }
            }
            
            str = sb.toString();
        }
        
        return str;
        
    }
}
```