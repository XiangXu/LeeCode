# 3Sum - (Medium)

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

## Solution

这道题我首先想到的方法是使用左右指针的方法来解决, 具体的步骤如下:

1. 首先我们先将数组按照从小到大的顺序来排序, 这样的话所给数组就变成了 -4, -1, -1, 0, 1, 2.
2. 然后声明一个Set用来过滤掉那些重复的组合.
3. 用一个for循环一次遍历数组中的每一个数, 比如从-4开始，然后声明两个指针分别指向-1和2.
4. 这个时候sum = -4 + -1 + 2 = -3,  值是小于0的于是我们需要将左指针向右移动来取得较大的值.
5. 如果sum是大于0的话，我们需要向左来移动右指针来取得一个较小的值.
6. 如果sum等于0的话，我们就直接创建一个list加入到set中.
7. 当我们遍历完所有的数字以后, 我们就可以直接返回结果了

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: 这里我们遍历了所给数组，并且使用了左右指针, 等于嵌套了两个for循环.
* **Space Complexity: O(n)**: 我们声明了一个set来存储最后的结果.

```java
class Solution 
{
    public List<List<Integer>> threeSum(int[] nums) 
    {
        if(nums == null || nums.length == 0 || nums.length < 3)
            return Collections.emptyList();
        
        Arrays.sort(nums);
        Set<List<Integer>> set = new HashSet<>();
        
        // -4, -1, -1, 0, 1, 2
        for(int i=0; i<nums.length-2; i++)
        {
            int left = i+1;
            int right = nums.length-1;
            
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum > 0)
                    right --;
                else if(sum < 0)
                    left ++;
                else
                {
                    set.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    right--;
                    left++;
                }
                    
            }

        }
        
        return new ArrayList<>(set);
    }
}
```

上面的解法呢其实没什么问题, 但是当我提交答案以后我发现太慢了! 于是我就想, 有没有什么办法能够提高速度呢?

其实很容易发现一个问题, 我们还是拿上面的那个数组来举例: -4, -1, -1, 0, 1, 2

其实在sum = -4 + -1 + 2 = -3 这个时候我们需要向右边来移动左指针, 但是下一位其实还是-1, 这样的话结果其实是一样的, 那么其实如果我们直接跳过想通的数字的话我们应该能节约很多时间.

而且如果我们跳过了相同的数字, 我们就不需要用set了, 因为最终的结果肯定是唯一的了! 理解了上面你的逻辑, 我们就可以更新我们的代码了, 应该还是挺直观的.

需要注意的一点是在拿当前数字的时候我们也需要判断是否等于前一个数字, 如果等于的话直接跳到下一个, 这样就避免了重复.

```java
if(i > 0 && nums[i] == nums[i-1])
    continue;
```

* **Time Complexity: O(n<sup>2</sup>)**: 这里我们遍历了所给数组，并且使用了左右指针, 等于嵌套了两个for循环.
* **Space Complexity: O(n)**: 我们声明了一个list来存储最后的结果.

```java
class Solution 
{
    public List<List<Integer>> threeSum(int[] nums) 
    {
        if(nums == null || nums.length == 0 || nums.length < 3)
            return Collections.emptyList();
        
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        
        // -4, -1, -1, 0, 1, 2
        for(int i=0; i<nums.length-2; i++)
        {
            if(i > 0 && nums[i] == nums[i-1])
                continue;
            
            int left = i+1;
            int right = nums.length-1;
            
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum > 0)
                {
                    right --;
                    while(left < right && nums[right] == nums[right+1])
                        right --;
                }
                    
                else if(sum < 0)
                {
                    left ++;
                    while(left < right && nums[left] == nums[left-1])
                        left++;
                }
                    
                else
                {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++;
                    right--;
                    
                    while(left < right && nums[right] == nums[right+1])
                        right --;
                    
                    while(left < right && nums[left] == nums[left-1])
                        left++;
                }
                    
            }

        }
        
        return result;
    }
}
```
