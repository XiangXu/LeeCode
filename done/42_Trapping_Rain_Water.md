# Trapping Rain Water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![alt text](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

Example:

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## Solution

首先我们需要思考的是形成积水的原因是什么? 当两边边框的高度都大于中间的高度时就会形成积水, 然后根据木桶原理我们知道, 积水高度取决于两个边框中高度较矮的那个. 

当前积水高度计算公式为: Math.min(height[left], height[right]) - height[current]

那么这道题就转换成了对于每一个点我们都需要找到左边和右边最高的边框, 在根据上面的公式就能算出当前点的积水量.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 我们首先对height数组进行了遍历, 然后我们用两个for循环来寻找maxLeft和maxRight.
* **Space Complexity: O(1)**: 用了一些变量而已.

```java
class Solution 
{   
    public int trap(int[] height) 
    {
        if(height == null || height.length == 0)
            return 0;
        
        int result = 0;
        
        // Water will never being trapped at index 0 and height.length-1
        for(int i=1; i<height.length-1; i++)
        {
            int maxLeft = 0;
            int maxRight = 0;
            
            for(int a=i; a>=0; a--)
            {
                maxLeft = Math.max(height[a], maxLeft); 
            }
            
            for(int b=i; b<height.length; b++)
            {
                maxRight = Math.max(height[b], maxRight);
            }
            
            result += Math.min(maxLeft, maxRight) - height[i];
        }
        
        return result;
    }
}
```

