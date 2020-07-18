#  Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place with O(1) extra memory**.

Example 1:

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

Example 2:

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

## Solution

这道题目感觉可以用双指针, 我们用两个指针left和right同时指向index为0的位置, 接下来我们首先向右移动right指针:
1. 如果right指针的数等于left指针的数, 我们就继续移动right.
2. 如果right指针的数不等于left指针的数, 说明这时候我们发现了一个新的数, 于是我们就将left++, 移动到下一位，然后nums[left] = nums[right], 这个时候我们就完成了替换, 然后继续移动right.
3. 一直重复上述的过程知道right移动到了最后一位, 这时候left值就是我们要的结果.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是nums数组的长度, 我们遍历了nums数组.
* **Space Complexity: O(1)**: 我们只声明了一些变量-两个指针.

```java
class Solution 
{    
    public int removeDuplicates(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return 0;
        
        int left = 0;
        int right = 0;
        
        while(right < nums.length)
        {
            if(nums[left] != nums[right])
            {
                nums[++left] = nums[right];
            }
            right ++;
        }
        
        return left+1;
    }
}
```