# Two Sum - (Easy)

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 解法 

这道题目主要在于使用HashMap来储存数组当前的值和数组的index, 具体步骤如下:

1. 我们可以遍历整个数组，然后用所给的taget减去数组中的每个数.
2. 如果数组中的key没有当前的差值,则当前数组的值和当前index存入HashMap的key和value.
3. 如果数组中的key有当前的差值，则直接返回当前for循环的i和HashMap中key对应的index.


## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 我们遍历来数组一遍，解法中包含来一个for循环.
* **Space Complexity: O(n)**: 我们用了一个HashMap来存储差值和index.

```java
class Solution 
{
    public int[] twoSum(int[] nums, int target) 
    {   
        if(nums == null || nums.length == 0)
            return nums;
        
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int i=0; i<nums.length; i++)
        {
            int tmp = target - nums[i];
           
            if(map.containsKey(tmp))
            {
                result[0] = i;
                result[1] = map.get(tmp);
            }    
            else
            {
                map.put(nums[i], i);
            }
        }
        
        return result;
    }
}
```