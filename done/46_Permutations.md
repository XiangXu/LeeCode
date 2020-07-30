# Permutations

Given a collection of distinct integers, return all possible permutations.

Example

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Solution

这道题可以用backtracking来做, 我们用一个for循环来遍历整个数组, 确定第一个开头的数字, 然后用backtracking的方式来补全后面的组合. 这里的难点就是如何实现不同的排列组合, 从题目中的列子来说如果我们确定了第一位是[1]以后, 我们如何得到[2,3]和[3,2]这两个组合. 这里就需要用到backtracking的思想了, 我们创建一个tmpList用来存储每一个组合, 然后遍历所给的数组. 如果当前tempList没有包含nums[i]的话就加进去, 然后进行递归调用, 最后再退一位.


## 空间时间复杂度分析:

* **Time Complexity: O(n!)**: 
* **Space Complexity: O(n)**: 声明了一个tempList来存储每一次符合条件的结果.

```java
class Solution 
{
    public List<List<Integer>> permute(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return Collections.emptyList();
        
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        
        if(nums.length == 1)
            tmpList.add(nums[0]);
        
        backTracking(tmpList, result, nums);
        
        return result;
        
    }
    
    private void backTracking(List<Integer> tmpList, List<List<Integer>> result, int[] nums)
    {        
        if(tmpList.size() == nums.length)
        {
            //we have to create a new list because tmpList will be modified afterwards.
            result.add(new ArrayList<>(tmpList));
            return;
        }
        
        for(int i=0; i<nums.length; i++)
        {
            int num = nums[i];
            
            if(tmpList.contains(num))
                continue;
            
            tmpList.add(num);
            backTracking(tmpList, result, nums);
            tmpList.remove(tmpList.size()-1);
        }
    }
}
```