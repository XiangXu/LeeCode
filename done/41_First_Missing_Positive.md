# First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

```
Input: [1,2,0]
Output: 3
```

Example 2:

```
Input: [3,4,-1,1]
Output: 2
```

Example 3:

```
Input: [7,8,9,11,12]
Output: 1
```

Note:

Your algorithm should run in O(n) time and uses constant extra space.

## Solution

这道题目第一次做的时候完全没有什么头绪, 想不到什么好的解法, 看了答案以后真的是感觉十分的巧妙, 是一个很锻炼思维的题目, 下面我们来讲解一下具体的思路.

这道题运用到了木桶排序(bucket sort)的思想, 关于木桶排序算法我会在我的Programming-Daily-Learning的repo算法中讲解这里就不详细说了.

这道题我们要明确一件事情, 我们需要找到数组中丢失的那个最小的正数, **假设数组的大小为3, 那么这个最小的正数一定是在0-4这个范围**, 这点需要理解.

因为这道题需要满足constant extra space, 一般要求这样的话我们就需要对当前的数组进行改动, 因为我们没有办法声明别内存来存储数据, 但是我们知道我们可以用多个for循环.

这里我们用到来数组的index, 这里有一个规律, **假设数组中的每个数是num, 那么如果我们按照index=num-1来排序数组中所有的正数, 随后遍历数组, 那么第一位我们发现index!=num的时候, 那个missing positive就应该是index+1**, 那么我们需要现将数组按照nums[nums[i]-1] == nums[i]来排序.

下面我们用题目中的三个例子来说:

```
array: 1, 2, 0
index: 0, 1, 2

1 - 0 = 0
2 - 1 = 1
0 - 1 != 2, 所以这里的答案就应该是2+1=3


array: 3, 4, -1, 1
index: 0, 1,  2, 3

i = 0: nums[3-1] = -1, nums[0] = 3, 不相等, 那么我们将3和-1互换, 数组变为 -1, 4, 3, 1;
i = 0: 此时当前的数为-1, i++;
i = 1: nums[4-1] = 1,  nums[1] = 4, 不相等, 那么我们将4和1互换, 数组变为 -1, 1, 3, 4;
i = 1: nums[1-1] = -1, nums[1] = 1, 不相等, 那么我们将-1和1互换, 数组变为1, -1, 3, 4;
i = 1: 此时当前的数为-1, i++;
i = 2: nums[3-1] = 3,  nums[2] = 3, 相等, i++;
i = 3: nums[4-1] = 4,  nums[3] = 4, 相等 结束;

这时候的数组为 1,-1, 3, 4, 我们遍历这个数组发现, index = 1的时候, -1 != index + 1 = 2, 那么这个最小正数就为2.
```

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是nums的长度.
* **Space Complexity: O(1)**: 用了一些变量

```java
class Solution 
{
    public int firstMissingPositive(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return 1;
        
        for(int i=0; i<nums.length; i++)
        {
            while(nums[i] > 0 && nums[i] <= nums.length && nums[nums[i]-1] != nums[i])
            {
                int tmp = nums[nums[i]-1];
                nums[nums[i]-1] = nums[i];
                nums[i] = tmp;
            }
                
        }
        
        for(int i=0; i<nums.length; i++)
        {
            if(nums[i] - 1 != i)
            {
                return i+1;
            }
                
        }
        
        return nums.length + 1;
    }
}
```



