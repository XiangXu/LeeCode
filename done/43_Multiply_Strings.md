# Multiply Strings

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.

Example 1:

```
Input: num1 = "2", num2 = "3"
Output: "6"
```

Example 2:

```
Input: num1 = "123", num2 = "456"
Output: "56088"
```

Note:

1. The length of both num1 and num2 is < 110.
2. Both num1 and num2 contain only digits 0-9.
3. Both num1 and num2 do not contain any leading zero, except the number 0 itself.
4. **You must not use any built-in BigInteger library or convert the inputs to integer directly**.

# Solution

这道题我们可以用到之前学过的一个技巧来做: num.charAt(0) - '0', 这样就能得到一个int类型, 我最开始的思路如下:

我们可以把结果分别放入两个数组中, 举个例子: num1Arr = [1,2,3]; nums2Arr[4,5,6], 然后我们按照正常乘法的规律走:
```
3 * 6 = 18; 2 * 6 = 12; 1 * 6 = 6 -> 18 + 12*10 + 6*100 = 738;
3 * 5 = 15; 2 * 5 = 10; 1 * 5 = 5 -> 15 + 10*10 + 5*100 = 615;
3 * 4 = 12; 2 * 4 = 8;  1 * 4 = 4 -> 12 + 8*10 + 4*100 = 492;
```
所以最终的结果: 738 + 615 * 10 + 492 * 100 = 56088.

但是这样是没办法通过testcase的, 比如说498828660196*840477629533, 超过了long的最大值, 所以这种解法是行不通的. 而且题目说明了不能用BigInteger, 怪自己看题不仔细.

看了discussion里面的一个答案(https://leetcode.com/problems/multiply-strings/discuss/17608/AC-solution-in-Java-with-explanation), 得到了启发:

首先两个数字相乘得到的结果的长度maxLen = num1.length() + num2.length(). 这样我们就能声明一个数组来记录每一位相乘的结果, 我们还是用[1,2,3]和[4,5,6]来举例:

首先声明一个数组 int[] products = new int[num1.length() + num2.length()], 然后我们还是以倒序的方式分别遍历两个数组, 那么products[i+j+1] += (num1.charAt(i)) - '0' * (num2.charAt(j) - '0');
```
i = 2, j = 2, int[5] = 18;
i = 2, j = 1, int[4] = 15;
i = 2, j = 0, int[3] = 12;
i = 1, j = 2, int[4] = 15 + 12 = 27;
i = 1, j = 1, int[3] = 12 + 10 = 22;
i = 1, j = 0, int[2] = 8;
i = 0, j = 2, int[3] = 22 + 6 = 18;
i = 0, j = 1, int[2] = 8 + 5 = 13;
i = 0, j = 0, int[1] = 4;

procusts = {0, 4, 13, 28, 27, 18}

然后我们还是以倒叙的方式遍历products, 每一位%10就是当前位数, /10的结果就是进位的值.

18 % 10 = 8, 18 / 10 = 1, 进1.
(27 + 1) % 10 = 8, 28 / 10 = 2, 进2.
(28 + 2) % 10 = 0, 20 / 10 = 3, 进2.
(13 + 3) % 10 = 6, 16 / 10 = 1, 进1.
(4 + 1) % 10 = 5, 5 / 10 = 0, 进0.

最终结果是56088
```

下面是具体实现的代码, 知道了解题思路以后还是比较直观的.


## 空间时间复杂度分析:

* **Time Complexity: O(mn)**: 我们遍历两个字符串中的字符, 所以时间复杂度应该为两个字符串相乘的结果.
* **Space Complexity: O(m+n)**: products数组来存储每两个字符串相乘的结果.

```java
class Solution 
{
    public String multiply(String num1, String num2) 
    {
        if("0".equals(num1) || "0".equals(num2))
            return "0";
        
        int len1 = num1.length();
        int len2 = num2.length();
        int sumLen = len1 + len2;
        
        int[] products = new int[sumLen];
        
        for(int i=len1-1; i>=0; i--)
        {
            for(int j=len2-1; j>=0; j--)
            {
                products[i+j+1] += (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
            }
        }
        
        StringBuilder sb = new StringBuilder();
        int carry = 0;
        
        for(int i=sumLen-1; i>=0; i--)
        {
            int total = products[i] + carry;
            int num = total % 10;
            carry = total / 10;
            sb.append(num);
        }
        
        String result = sb.reverse().toString();
        if(result.charAt(0) == '0')
            result = result.substring(1, result.length());
        
        return result;
    }
}
```