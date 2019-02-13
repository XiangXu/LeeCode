# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

## First Solution

Try to loop through all the nums and add them together 

Runtime: **45 ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] indices = new int[2];
		
		for(int i=0; i<nums.length; i++)
		{
			for(int j=i+1; j<nums.length; j++)
			{
				if(nums[i] + nums[j] == target)
				{
					indices[0] = i;
					indices[1] = j;
					break;
				}
			}
		}
		
		return indices;
    }
}
```

## Second Solution

Instead of looping array twice, we can just loop array once by using a HashMap to store the index and complement.

Runtime: **3 ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) 
    {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int i=0; i<nums.length; i++)
        {
            int complement = target - nums[i];
            if(map.containsKey(complement))
            {
                return new int[]{ map.get(complement), i };
            }
            
            map.put(nums[i], i);
        }
        
        throw new IllegalArgumentException("No two sum solution");
    }
}

```
