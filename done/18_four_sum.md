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

## Solution

这道题的解题思路其实和3Sum是异曲同工的, 唯一的区别就是这里需要用2个for循环来确定第一个数和第二个数, 然后剩下的逻辑其实都是一样的, 这里就不再重新叙述了.

这里有一个小技巧是在第二个for循环中, 判断下一个数字是否与上一个数相同的时候请注意

```java
if(j > i+1 && nums[j] == nums[j-1])
    continue;
```

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup></sup>)**: 这里确定第一个和第二个数的两个for循环加上里面的while循环.
* **Space Complexity: O(n)**: 定义了一个list来存储结果, n的话为最总结果的长度.

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) 
    {
        if(nums == null || nums.length < 4)
            return Collections.emptyList();
        
        Arrays.sort(nums);
        
        List<List<Integer>> result = new ArrayList<>();
        
        //-2 -2 -1 -1 0 0 1 2 
        for(int i=0; i<nums.length-3; i++)
        {
            if(i>0 && nums[i] == nums[i-1])
                continue; 
            
            for(int j=i+1; j<nums.length-2; j++)
            {
                if(j > i+1 && nums[j] == nums[j-1])
                    continue;
                
                int firstNum = nums[i];
                int secondNum = nums[j];
                int left = j+1;
                int right = nums.length-1;
  
                while(left < right)
                {
                    int sum = firstNum + secondNum + nums[left] + nums[right];
                    
                    if(sum < target)
                    {
                        left ++;
                        while(left < right && nums[left] == nums[left-1])
                            left++;
                    }
                    if(sum > target)
                    {
                        right --;
                        while(left < right && nums[right] == nums[right+1])
                            right--;
                    }
                    else if(sum == target)
                    {
                        result.add(Arrays.asList(firstNum, secondNum, nums[left], nums[right]));
                        
                        left++;
                        while(left < right && nums[left] == nums[left-1])
                            left++;
                       
                        right--;
                        while(left < right && nums[right] == nums[right+1])
                            right--;
                    }
                }
            }
        }
        
        return result;
    }
}
```

