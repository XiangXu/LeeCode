# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

## Approach 1: Brute Force

Loop through each elements x and find if there is another value that equals to target - x.

Runtime: **45 ms**
Memory: **39 MB**

```java
class Solution 
{
    public int[] twoSum(int[] nums, int target) 
    {
        for(int i=0; i<nums.length; i++)
        {
            for(int j=i+1; j<nums.length; j++)
            {
                if(nums[i] + nums[j] == target)
                {
                    return new int[] { i, j };
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    } 
}
```

### Complexity Analysis

Time Complexity: O(n2)  
Space complexity: O(1)


## Approach 2: Two-pass Hash Table

In the first iteration, we add each element's value and its index to the table.
In the second iteration, if each element's complement exists in the table. Beware that the complement must not be nums[i] itself.

Runtime: **2 ms**
Memory: **41 MB**

```java
class Solution 
{
    public int[] twoSum(int[] nums, int target) 
    {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int i=0; i<nums.length; i++)
        {
            map.put(nums[i], i);
        }
        
        for(int i=0; i<nums.length; i++)
        {
            int complement = target - nums[i];
            if(map.containsKey(complement) && map.get(complement) != i)
            {
                return new int[] { i, map.get(complement)};
            }
        }
        
        
        throw new IllegalArgumentException("No two sum solution");
    } 
}
```

### Complexity Analysis

Time Complexity: O(n)  
Space complexity: O(n)


## Approach 3: One-pass Hash Table

While we iterate and inserting elements into the table, we also look back to check if current element's compelment already exists in the table. If it exists, we have found a solution and return immdediately.

Runtime: **1 ms**
Memory: **42.2 MB**

```java
class Solution 
{
    public int[] twoSum(int[] nums, int target) 
    {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int i=0; i<nums.length; i++)
        {
            int complement = target - nums[i];
            
            if(map.containsKey(complement))
            {
                return new int[]{i, map.get(complement)};
            }
            
            map.put(nums[i], i);
        }
        
        throw new IllegalArgumentException("No two sum solution");
    } 
}
```

### Complexity Analysis

Time Complexity: O(n)  
Space complexity: O(n)
