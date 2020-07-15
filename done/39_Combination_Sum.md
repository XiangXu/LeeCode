# Combination Sum

Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

Example 1:

```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

Example 2:

```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

Constraints:

* 1 <= candidates.length <= 30
* 1 <= candidates[i] <= 200
* Each element of candidate is unique.
* 1 <= target <= 500

## Solution

这道题感觉和17题的题意有相识之处的, 这种题目要拿到所有组合的可能性一看就是要用DFS, 我们需要一层一层的遍历所有的组合. 我们从17题中学到了我们需要使用for循环.

这里总结一下这样题目的规律:

1. 首先我们肯定需要定义一个index来存储当前的index值.
2. 我们需要用一个容器来存储当前遍历过的元素, 这里用了一个list来存储的是元素之和.
3. 我们还需要在for循环中使用递归, 这样就能拿到所有的组合.
4. 递归方法的第一步一定是来check一些条件来跳出递归.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是值candidates中所有组合的总和.
* **Space Complexity: O(n)**: 定义了一个list来存储结果, 另外一个temList用来存储当前的元素, n的话为较长的那个list的长度.


```java
class Solution 
{
    public List<List<Integer>> combinationSum(int[] candidates, int target) 
    {
        if(candidates == null || candidates.length == 0)
            return Collections.emptyList();
        
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        
        dfs(0, tempList, candidates, target, result);
        
        return result;
    }
    
    
    private void dfs(int index, List<Integer> tempList, int[] candidates, int target, List<List<Integer>> result)
    {
        if(target <= 0)
        {
            if(target == 0)
                result.add(new ArrayList<>(tempList));
            
            return;
        }
        
        for(int i=index; i<candidates.length; i++)
        {
            tempList.add(candidates[i]);
            dfs(i, tempList, candidates, target-candidates[i], result);
            tempList.remove(tempList.size()-1);
        }
    }
}
```