# 3Sum Closest

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

## First solution
Use 3 pointers to point current element, next element and the last element. If the sum is less than target, it means we have to add a larger element so next element move to the next. If the sum is greater, it means we have to add a smaller element so last element move to the second last element. Keep doing this until the end. Each time compare the difference between sum and target, if it is less than minimum difference so far, then replace result with it, otherwise keep iterating.

Runtime: **5 ms**

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int result = nums[0] + nums[1] + nums[nums.length-1];
        for(int i=0; i<nums.length; i++)
        {
            int left = i+1;
            int right = nums.length-1;
            while(left < right)
            {
                int newResult = nums[i] + nums[left] + nums[right];
                int diff = target - newResult;
                result = Math.abs(target-result) < Math.abs(target - newResult) ? result : newResult;
                if(diff > 0)
                {
                    left++;
                }
                else if(diff < 0)
                {
                    right--;
                }
                else
                {
                    return result;
                }
            }
        }
        return result;
    }
}
```
