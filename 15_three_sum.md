# 3Sum

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
```
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## First Solution

Use a Set<List<Integer>> to remove duplicate triplets

Runtime: **386 ms**

Memory: **43.9 MB**

```java
class Solution 
{
    // 
    public List<List<Integer>> threeSum(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return Collections.emptyList();
        
        Set<List<Integer>> set = new HashSet<>();
        Arrays.sort(nums);
        // -4, -1, -1, 0, 1, 2
        for(int i=0; i<nums.length-2; i++)
        {
            int a = i + 1;
            int b = nums.length - 1;
            while(a < b)
            {
                int sum = nums[i] + nums[a] + nums[b];
                if(sum == 0)
                    set.add(Arrays.asList(nums[i], nums[a++], nums[b--]));
                else if(sum < 0)
                    a++;
                else
                    b--;
            }               
        }
        
        return new ArrayList<>(set);
    }
}
```

**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(n)**

## Second Solution

Use while loop to skip duplicate

Runtime: **24 ms**

Memory: **42.8 MB**

```java
class Solution 
{
    // 
    public List<List<Integer>> threeSum(int[] nums) 
    {
        if(nums == null || nums.length < 3)
            return Collections.emptyList();
        
        Arrays.sort(nums);  
        int length = nums.length;
        List<List<Integer>> result = new ArrayList<>();
        
        // -4, -1, -1, 0, 1, 2
        for(int i=0; i<length-2; i++)
        {            
            if(i > 0 && nums[i] == nums[i-1])
                continue;
            
            int left = i+1;
            int right = length-1;
           
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum < 0)
                {
                    left ++;
                    while(left < right && nums[left] == nums[left-1])
                        left ++;
                }
                else if(sum > 0)
                {
                    right --;
                    while(left < right && nums[right] == nums[right+1])
                        right --;
                }
                else
                {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left ++;
                    right --;
                    while(left < right && nums[left] == nums[left-1])
                        left ++;
                    while(left < right && nums[right] == nums[right+1])
                        right --;
                }
            }
            
        }
        
        return result;
    }
}
```

**Time Complexity: O(n<sup>2</sup>)**

**Space Complexity: O(1)**