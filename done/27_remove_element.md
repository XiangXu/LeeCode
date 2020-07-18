# Remove Element

Given an array nums and a value val, remove all instances of that value **in-place** and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**The order of elements can be changed**. It doesn't matter what you leave beyond the new length.

Example 1:

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

Example 2:

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

## Solution

我在开始做的时候不知道为什么总是想到将数组排序, 把简单的问题弄的复杂化了. 其实简单的使用双指针就能轻松解决这道题.
1. 我们首声明两个指针left和right分别指向index为0的位置, 然后用right来进行for循环.
2. 如果当前nums[right] != val的话, 我们就将nums[left] = nums[right].

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是nums数组的长度, 我们遍历了nums数组.
* **Space Complexity: O(1)**: 我们只声明了一些变量-两个指针.

```java
class Solution 
{
    
    public int removeElement(int[] nums, int val) 
    {
        if(nums == null || nums.length == 0)
            return 0;
        
        int left = 0;
        for(int right=0; right<nums.length; right++)
        {
            if(nums[right] != val)
                nums[left++] = nums[right];
        }
        
        return left;
    }
}
```