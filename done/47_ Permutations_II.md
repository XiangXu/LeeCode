#  Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

Example

```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## Solution

这道题开始我还是考虑用backtracking的思想做, 但是由于数组中有重复的数字, 所以我们需要转换思路来做.

首先我们要考虑我们怎么去重. 在上一题中我们直接用list.contains来做, 这里显然是不可以了. 既然我们不能用数字本身来去重, 那么我们可以用什么呢? 答案是数组的
index!, 我们可以用一个boolean[]的数组来记录每一位是否已经访问. 接下来我们要考虑的问题就是如果避免重复的数字产生重复的结果, 拿题目所给的input来举个例子:
```
nums = [1, 1, 2]
当index = 0的时候, 我们能产生[1, 1, 2]
当index = 1的时候, 我们还是能产生[1, 1, 2] 
```
出现这个情况的原因是因为在index=0和index=1的情况下, nums数组中对应的数字都是1. 我们要做的是如果当前数字已经用过了的话我们需要跳过, 具体的实现方法大概是: 
```java
//handle duplicate numbers, if previous identical number is used, then use the current number.
if((i > 0 && nums[i] == nums[i-1]) && !visited[i-1]) continue; 
```
要做到这样的话, 前提是所有重复的数字都在相邻的位置, 我们可以通过排序来取得这样的效果.

## 空间时间复杂度分析:

* **Time Complexity: O(n!)**: 
* **Space Complexity: O(n)**: 声明了一个tempList来存储每一次符合条件的结果. visited数组来存储visited的index.

```java
class Solution 
{
    public List<List<Integer>> permuteUnique(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return Collections.emptyList();
        
        Arrays.sort(nums);
        
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        
        // This array used to track visited index
        boolean[] visited = new boolean[nums.length];
        
        backTracking(visited, nums, tmpList, result);
        
        return result;
    }
    
    private void backTracking(boolean[] visited, int[] nums, List<Integer> tmpList, List<List<Integer>> result)
    {
        if(tmpList.size() == nums.length)
        {
            //tmpList will be modified afterwards, so we need to create a copy of it
            result.add(new ArrayList<>(tmpList));
            return;
        }
        
        for(int i=0; i<nums.length; i++)
        {
            if(visited[i]) 
                continue;
            
            //handle duplicate numbers, if previous identical number is used, then use the current number.
            if((i > 0 && nums[i] == nums[i-1]) && !visited[i-1])
                continue;
            
            tmpList.add(nums[i]);
            visited[i] = true;
            backTracking(visited, nums, tmpList, result);
            tmpList.remove(tmpList.size()-1);
            visited[i] = false;
        }
    }
}
```