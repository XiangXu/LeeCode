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

Brute force

Runtime: **694 ms**

```java

class Solution 
{
    public List<List<Integer>> fourSum(int[] nums, int target) 
    {
        List<List<Integer>> results = new ArrayList<>();
        
        if(nums == null || nums.length < 4)
            return results;
        
        Arrays.sort(nums);
        
        Map<String, String> trackingMapper = new HashMap<>();
        
        for(int a=0; a<nums.length; a++)
        {
            for(int b=a+1; b<nums.length; b++)
            {
                for(int c=b+1; c<nums.length; c++)
                {
                    for(int d=c+1; d<nums.length; d++)
                    {
                        if(nums[a]+nums[b]+nums[c]+nums[d] == target)
                        {
                            String key = String.valueOf(nums[a])+String.valueOf(nums[b])+   String.valueOf(nums[c])+String.valueOf(nums[d]);
                            
                            if(trackingMapper.containsKey(key)){
                                continue;
                            }
                            else
                            {
                                trackingMapper.put(key, "");
                                List<Integer> tempList = new ArrayList<>();
                                tempList.add(nums[a]);
                                tempList.add(nums[b]);
                                tempList.add(nums[c]);
                                tempList.add(nums[d]);
                                results.add(tempList);    
                            }
                            
                        }
                    }
                }
                    
            }
        }
        return results;
    }
}

```
