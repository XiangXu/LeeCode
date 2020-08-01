# Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:

```
Input: [1,3,5,6], 5
Output: 2
```

Example 2:

```
Input: [1,3,5,6], 2
Output: 1
```

Example 3:

```
Input: [1,3,5,6], 7
Output: 4
```

Example 4:

```
Input: [1,3,5,6], 0
Output: 0
```

## Solution 

这道题目所给的条件是一个排序无重复的数组, 要我们找到所给target的index或者是适合插入的index, 很显然我们需要用Binary Search来做.
具体思路如下:
1. 按照正常的Binary Search来查找target, 这里我们不用递归来做.
2. 如果我们发现了target, 那么直接就返回index.
3. 如果没有发现target, 那么结果就是start.

其实感觉这道题目考的就是对于Binary Search的理解.

## 空间时间复杂度分析:

* **Time Complexity: O(logn)**: 这里用了binary search来做.
* **Space Complexity: O(1)**: 声明了一些变量.

```java
class Solution 
{
    public int searchInsert(int[] nums, int target) 
    {
        if(nums == null || nums.length == 0)
            return -1;
        
        int start = 0;
        int end = nums.length-1;
        
        while(start <= end)
        {
            int mid = start + (end - start) / 2;
            
            if(nums[mid] > target)
            {
                end = mid - 1;
            }
            else if(nums[mid] < target)
            {
                start = mid + 1;
            }
            else
            {
                return mid;
            }
        }
        
        return start;
    }
}
```
