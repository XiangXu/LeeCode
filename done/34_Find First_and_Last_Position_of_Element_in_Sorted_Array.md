# Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

Example 1:

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

Example 2:

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

Constraints:

* 0 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9
* nums is a non decreasing array.
* -10^9 <= target <= 10^9

## Solution

从题目中知道这个数组是排序的数组而且答案要求我们的解法时间复杂度必须符合O(log n), 那么我们可以得出这道题我们需要使用Binary Search来解决. 现在的问题是我们如何用binary Search来找到target的起点和终点. 这里可以将Binary Search的算法稍微修改以下:
1. 为了要拿到起点, 就算我们通过了Binary Search拿到了结果, 我们还是要继续通过缩小end来缩小范围.
2. 为了要拿到终点, 就算我们通过了Binary Search拿到了结果, 我们还是要继续通过增加start来缩小范围.

```java
class Solution 
{
    public int[] searchRange(int[] nums, int target) 
    {
        if(nums == null || nums.length == 0)
            return new int[]{-1, -1};
    
        int start = findStartIndex(nums, target);
        int end = findEndIndex(nums, target);
        
        return new int[]{start, end};
    }
    
    private int findStartIndex(int[] nums, int target)
    {
        int start = 0;
        int end = nums.length-1;
        int index = -1;
        
        while(start <= end)
        {
            int mid = start + (end - start) / 2;
            if(nums[mid] >= target)
                end = mid - 1;
            else 
                start = mid + 1;
            
            if(nums[mid] == target)
                index = mid;
            
            System.out.println(start + " " + end);
        }
        
        return index;
    }
    
    private int findEndIndex(int[] nums, int target)
    {
        int start = 0;
        int end = nums.length-1;
        int index = -1;
        
        while(start <= end)
        {
            int mid = start + (end - start) / 2;
            if(nums[mid] <= target)
                start = mid + 1;
            else 
                end = mid - 1;
            
            if(nums[mid] == target)
                index = mid;
        }
        
        return index;
    }
}
```