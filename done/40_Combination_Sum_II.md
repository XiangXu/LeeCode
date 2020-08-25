# Combination Sum II

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

Example 1:

```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

Example 2:

```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

## Solution

这道题其实和39题的思路基本差不多, 唯一的区别就是这里不能重复, 一般不能重复的问题我们就要考虑到排序.

这里我们首先将所给数组排序, 那么 2,5,2,1,2就会变成 1,2,2,2,5

然后我们依次遍历数组就可以了, 如果懂了39题的话这道题其实并不难.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是值candidates中所有组合的总和.
* **Space Complexity: O(n)**: 定义了一个list来存储结果, 另外一个temList用来存储当前的元素, n的话为较长的那个list的长度.


```java
class Solution 
{
    public List<List<Integer>> combinationSum2(int[] candidates, int target) 
    {
        if(candidates == null || candidates.length == 0)
            return Collections.emptyList();
        
        Arrays.sort(candidates);
        
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        
        backTracking(0, tempList, candidates, target, result);
        
        return result;
        
    }
    
    private void backTracking(int index, List<Integer> tempList, int[] candidates, int target, List<List<Integer>> result)
    {
        if(target <= 0)
        {
            if(target == 0)
                result.add(new ArrayList<>(tempList));
            
            return;
        }
        
        // 1,1,2,5,6,7,10
        // 1,2,2,2,5
        for(int i=index; i<candidates.length; i++)
        {   
            if(i > index && candidates[i] == candidates[i-1])
                continue;
            
            tempList.add(candidates[i]);
            backTracking(i+1, tempList, candidates, target - candidates[i], result);
            tempList.remove(tempList.size()-1);
        }
    }
}
```