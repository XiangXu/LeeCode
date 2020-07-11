# Product of Array Except Self - (Medium)

Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

Constraint: It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.

**Note: Please solve it without division and in O(n)**.

Follow up:

Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

## Solution

这道题我第一次看到是完全没有头绪的. 看了答案以后恍然大悟, 其实这道题就是从左乘到右，再从右乘到左, 下面用一个例子来解释.

```
假设我们的input为:

4     5     1     2     8

我们将第一个位设为1, 从左到右开始依次乘法

1     4     20    20    160

我们将第最后个位设为1, 从右到左开始依次乘法

80    16    16     8     1       

这样最终的结果就是这两个数组每一位分别相乘.

80    64    320    160   160
```

这样的话其实就一目了然来, 我们用1来形成一个错位. 以1为例子, 1左边相乘的结果就是20其实就是左到右相乘的结果, 1右边相乘的结果就是16其实就是右到左相乘的结果. 这样最终的结果就是320.

下面我们来实现一个这个逻辑:

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里遍历所给数组需要n的时间.
* **Space Complexity: O(n)**: 这里我们用了两个数组来存储相乘的结果.

```java
class Solution 
{
    public int[] productExceptSelf(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return nums;
        
        int len = nums.length;
        int[] leftProduct = new int[len];
        int[] rightProduct = new int[len];
        
        int[] result = new int[len];
        
        leftProduct[0] = 1;
        rightProduct[len-1] = 1;
        
        for(int i=1; i<len; i++)
        {
            leftProduct[i] = nums[i-1] * leftProduct[i-1];
        }
        
        for(int i=len-2; i>=0; i--)
        {
            rightProduct[i] = nums[i+1] * rightProduct[i+1];
        }
        
        
        for(int i=0; i<len; i++)
        {
            result[i] = leftProduct[i] * rightProduct[i];
        }
        
        
        return result;
    }
}
```

在follow up中要求我们将解法提高到只用O(1), 那么我们会想能不能用result数组来取代掉leftProduct和rightProduct呢?

```java
class Solution 
{
    public int[] productExceptSelf(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return nums;
        
        int len = nums.length;
        int[] result = new int[len];
        
        result[0] = 1;
        
        for(int i=1; i<len; i++)
        {
            result[i] = nums[i-1] * result[i-1];
        }
        
        int tmp = 1;
        for(int i=len-1; i>=0; i--)
        {
            result[i] = result[i] * tmp;
            tmp = tmp * nums[i];
        }
        
        
        return result;
    }
}
```

