# 3Sum Closest

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

## First solution

Runtime: **4 ms**

Memory: **39 MB**

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) 
    {
        if(nums == null || nums.length < 3)
            return 0;
        
        Arrays.sort(nums);
        //-4  -1  1  2
        int result = nums[0] + nums[1] + nums[nums.length - 1];
        
        for(int i=0; i<nums.length-2; i++)
        {
            int left = i+1;
            int right = nums.length - 1;
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum == target)
                    return sum;
                else if(sum > target)
                    right --;
                else 
                    left ++;
                
                if(Math.abs(sum - target) < Math.abs(result - target))
                    result = sum;
            }
        }
        
        return result;
    }
}
```

**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(1)**
