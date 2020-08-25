# Pow(x, n)

Implement pow(x, n), which calculates x raised to the power n (i.e. x<sup>n</sup>).

```
Example 1:

Input: x = 2.00000, n = 10
Output: 1024.00000

Example 2:

Input: x = 2.10000, n = 3
Output: 9.26100

Example 3:

Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

Constraints:

* -100.0 < x < 100.0
* -231 <= n <= 231-1
* -104 <= xn <= 104

## Solution

拿到这道题我最先想到的方法是直接用一个for循环来做乘法, 直到得到结果,然而不出所料太慢了, 得到TLE.

```java
class Solution 
{
    public double myPow(double x, int n) 
    {
        if(n > 0)
            return pow(x, n);
        else
            return 1.0 / pow(x, -n);
    }
    
    private double pow(double x, int n)
    {        
        if(n == 0)
            return 1;
        
        double result = x;
        for(int i=0; i<n-1; i++)
        {
            result *= x;
        }
        
        return result;
    }
}
```

此时的时间复杂度为O(n), 我们需要思考一下如何提升.

下面我们看几个例子:

1. x = 2, n = 1, result = 2;
2. x = 2, n = 2, result = 2 * 2 = 4;
3. x = 2, n = 3, result = 2 * 2 * 2 = 8;
4. x = 2, n = 4, result = 2 * 2 * 2 * 2 = 16;
5. x = 2, n = 5, result = 2 * 2 * 2 * 2 * 2 = 32;

如果乘法的话，我们不用一次一次的相乘，得到 2 次方后，我们可以直接把 2 次方的结果相乘，就可以得到 4 次方，得到 4 次方的结果再相乘，就是 8 次方了，这样的话就会快很多了。 我们的思路就是：

1. 如果 n 是偶数，我们将 n 折半，底数变为 x^2
2. 如果 n 是奇数， 我们将 n 减去 1 ，底数不变，得到的结果再乘上底数 x

## 空间时间复杂度分析:

* **Time Complexity: O(logN)**
* **Space Complexity: O(1)**

```java
class Solution 
{
    public double myPow(double x, int n) 
    {      
        //handle special case:
        // 2.00000
        // -2147483648
        if(n == Integer.MIN_VALUE && x > 1)
            return 0;
        
        if(n < 0)
            return 1 / pow(x, -n);
        else
            return pow(x, n);
    }
    
    private double pow(double x, int n)
    {
        if(n == 0)
            return 1;
        
        if(n == 1)
            return x;
        
        if(n % 2 == 0)
            return pow(x * x, n / 2);
        else
            return x * pow(x * x, n / 2);
    }
}
```
