# 3Sum Closest

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

## Solution

这道题其实和上一道题差不多的, 这里就不再过多的解释了.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 这里我们遍历了所给数组，并且使用了左右指针, 等于嵌套了两个for循环.
* **Space Complexity: O(1)**: 我们声明了一些变量来存储结果.

```java
class Solution 
{
    public int threeSumClosest(int[] nums, int target) 
    {
        if(nums == null || nums.length == 0 || nums.length <3)
            return target;
        
        Arrays.sort(nums);

        int diff = nums[0] + nums[1] + nums[nums.length-1];
        
        for(int i=0; i<nums.length-2; i++)
        {
            if(i>0 && nums[i] == nums[i-1])
                continue;
            
            int left = i+1;
            int right = nums.length - 1;
            
            // -4 -1 1 2 
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(Math.abs(target - sum) < Math.abs(target-diff))
                    diff = sum;
                
                if(sum > target)
                {
                    right --;
                    while(left < right && nums[right] == nums[right+1])
                        right --;
                }
                else if(sum < target)
                {
                    left ++;
                    while(left < right && nums[left] == nums[left-1])
                        left++;
                }
                else
                {
                    return sum;
                }
            }
        }
        
        return diff;
    }
}
```