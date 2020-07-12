# Container With Most Water

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

![alt text](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.

## Solution

刚开始看看这道题其实就想到了暴力破解法, 拿到所有的可能性然后取最大的值. 看了答案以后一目了然, 具体实现思路如下:

面积 = 长 * 宽

我们使用两个指针left和right, 分别指向所给数组的最左边和最右边. 这个时候长就是right - left. 

下面我们来分析一下宽, 宽其实就是两个指针所指数组中的较小的那个数, 这个时候我们可以计算出一个面积. 然后我们需要移动left或者right, 但是我们移动哪一呢? 

我们这样思考, 不管移动哪一个, 数组的长度都会变小, 那么我们需要移动此时指向较小的那个数, 这样我们才有可能取得一个较大的宽来增大面积.

依次这样最总我们就能得到答案了.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 我们用两个指针从左到右一次移动一个来遍历数组.
* **Space Complexity: O(1)**: 只声明了一些变量

```java
class Solution 
{
    public int maxArea(int[] height) 
    {
        if(height == null || height.length == 0)
            return 0;
        
        int left = 0;
        int right = height.length-1;
        int maxArea = Integer.MIN_VALUE;
        
        while(left < right)
        {
            int currWidth = right - left;
            int currHeight;
            
            if(height[left] > height[right])
            {
                currHeight = height[right];
                right --;
            }
            else 
            {
                currHeight = height[left];
                left ++;
            }
                
            maxArea = Math.max(maxArea, currWidth * currHeight);
        }
             
        return maxArea;
    }
}
```







