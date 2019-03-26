# Container With Most Water

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.

## First Solution
In this case, we will simply consider the area for every possible pair of the lines and find out the maximum area out of those.

Runtime: **224 ms**

```java

class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        
        if(height.length < 2)
            return maxArea;
        
        for(int i=0; i<height.length; i++)
        {
            for(int j=i+1; j<height.length; j++)
            {
                maxArea = Math.max(maxArea, Math.min(height[i], height[j]) * (j - i));
            }
        }
        
        return maxArea;
    }
}

```
