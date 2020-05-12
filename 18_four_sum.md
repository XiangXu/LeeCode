# 4Sum

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such that a + b + c + d = target? 
Find all unique quadruplets in the array which gives the sum of target.

Note:

The solution set must not contain duplicate quadruplets.

Example:

Given array nums = [1, 0, -1, 0, -2, 2], and target = 0.  
  
A solution set is:  
[  
  [-1,  0, 0, 1],  
  [-2, -1, 1, 2],  
  [-2,  0, 0, 2].   
]

## First Solution

Use while loop to skip duplicate

Runtime: **19 ms**

Memory: **40 MB**


```java
class Solution 
{
    public List<List<Integer>> fourSum(int[] nums, int target) 
    {
        if(nums == null || nums.length < 4)
            return Collections.emptyList();
        
        Arrays.sort(nums);
        int length = nums.length;
        
        List<List<Integer>> result = new ArrayList<>();
        
        for(int i=0; i<length-3; i++)
        {
            if(i > 0 && nums[i] == nums[i-1])
                continue;
            
            for(int j=i+1; j<length-2; j++)
            {
                if(j > i+1 && nums[j] == nums[j-1])
                    continue;
                
                int left = j + 1; 
                int right = length - 1;
                
                while(left < right)
                {
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];
                    if(sum < target)
                    {
                        left ++;
                        while(left < right && nums[left] == nums[left-1])
                            left ++;
                    }
                    else if(sum > target)
                    {
                        right --;
                        while(left < right && nums[right] == nums[right+1])
                            right --;
                    }
                    else if(sum == target)
                    {
                        result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));                
                        left ++;
                        right --;
                        
                        while(left < right && nums[left] == nums[left-1])
                            left ++;
                        while(left < right && nums[right] == nums[right+1])
                            right --;
                    }
                }
            }
        }
        
        return result;
    }
}
```

**Time Complexity: O(n<sup>3</sup>)**

**Space Complexity: O(n)**
