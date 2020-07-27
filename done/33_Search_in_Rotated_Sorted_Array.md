# Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

Example 2:

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

## Solution

看题目题意我们知道所给数组是递增排列的而且解决这道题目要求的时间复杂度为: O(logn), 那么我们就应该是要用binary search. 我们首先需要找到pivot, 这个点至关重要, 因为拿到这个点以后, 我们就可以决定是在这个点之前还是之后用binary search. 那么接下来的问题是如何找到这个pivot呢, 其实也是可以用binary search来找的.

举个例子: nums = [4,5,6,7,8,0,1,2], raget = 5.
我们首先对数组进行binary search, 比较nums[middle]和nums[right]的大小, 具体如下:
1. left = 0; right = 7; middle = 0 + (7 - 0) / 2 = 3; 此时nums[middle] = 7 大于 nums[right] = 2; right = middle; left = middle + 1 = 4.
2. left = 4; right = 7, middle = 4 + (7 - 4) / 2 = 5; 此时nums[5] = 0, 此时nums[5] 小于 nums[right] = 2; right = middle = 4. 得到pivot的index为4.
3. 比较target和nums[0] = 4; 4 < 5, 所以我们就在index 0到4之前进行binary search得到最终的结果.

## 空间时间复杂度分析:

* **Time Complexity: O(logn)**: 这里用binary search来找到pivot和target.
* **Space Complexity: O(1)**: 我们这里只声明了一些变量.

```java
class Solution 
{        
    public int search(int[] nums, int target) 
    {
        if(nums == null || nums.length == 0)
            return -1;
        
        int pivot = findPivot(nums);
        
        if(nums[pivot] == target) 
            return pivot;
        
        int left = (target > nums[nums.length-1]) ? 0 : pivot;
        int right = (target > nums[nums.length-1]) ? pivot-1 : nums.length-1;
        
        return binarySearch(left, right, nums, target);   
    }
    
    private int binarySearch(int left, int right, int[] nums, int target)
    {
        if(left > right)
            return -1;
        
        int middle = left + (right - left) / 2;
        
        if(nums[middle] == target)
            return middle;
        else if(nums[middle] > target)
            return binarySearch(left, middle-1, nums, target);
        else
            return binarySearch(middle+1, right, nums, target);
    }
    
    private int findPivot(int[] nums)
    {
        int left = 0;
        int right = nums.length-1;
        
        while(left < right)
        {
            int middle = left + (right - left) / 2;
            
            if(nums[middle] > nums[right])
                left = middle + 1;
            else
                right = middle;
        }
        
        return left;
    }
}
```