# Palindrome Number - (Easy)

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:
```
Input: 121
Output: true
```

Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Follow up:

Coud you solve it without converting the integer to a string?

## Solution

这道题没有太大的难度, 判断一个数是不是回文其实我们只要将这个数反转过来, 如果反转以后的结果还一样, 那么这个数字就是回文.

## 空间时间复杂度分析:

* **Time Complexity: O(logn)**: 每次将所给数字除以10.
* **Space Complexity: O(1)**: 只声明了一些变量.

```java
public class Solution 
{
    public boolean isPalindrome(int x) 
    {   
        if(x < 0)
            return false;
        
        if(x >=0 && x <= 9)
            return true;
        
        int reverse = 0;
        int tmp = x;
        
        while(tmp > 0)
        {
            reverse = reverse * 10 + tmp % 10;
            tmp = tmp / 10;
        }
        
        return x == reverse;
    }
}
```

