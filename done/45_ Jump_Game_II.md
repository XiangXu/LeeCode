#  Jump Game II

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

Example:

```
Input: [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
Note:

You can assume that you can always reach the last index.

# Solution

这道题拿到题目以后我的第一反应就是用BFS的思想来做, 做完提交以后发现偶尔会TLE, 思路还是挺清晰的.

## 空间时间复杂度分析:

* **Time Complexity: O(n<sup>2</sup>)**: BFS的时候嵌套了两个循环来loop数组的index.
* **Space Complexity: O(n)**: 声明了一个queue和visited数组.

```java
class Solution 
{
    public int jump(int[] nums) 
    {
        if(nums == null || nums.length < 2)
            return 0;
        
        int len = nums.length;
        boolean[] visited = new boolean[len];
        Queue<Integer> queue = new LinkedList<>();
        
        queue.offer(0);
        visited[0] = true;
        int steps = 0;
        
        while(!queue.isEmpty())
        {
            int size = queue.size();
            for(int i=0; i<size; i++)
            {
                int index = queue.poll();
                if(index >= len-1)
                    return steps;
                
                for(int j=1; j<=nums[index]; j++)
                {
                    int nextIndex = j + index;
                    if(nextIndex > len - 1)
                        break;
                    
                    if(visited[nextIndex])
                        continue;
                    
                    queue.offer(nextIndex);
                    visited[nextIndex] = true;
                }
            }
            
            steps ++;
        }
        
        return -1;
        
    }
}
```

但是上面的方法是在是太慢了, 在我看了答案以后学习了一个新的算法Greedy Algorithm

https://github.com/XiangXu/Programming-Daily-Learning/blob/master/Algorithm/3_Greedy_Algorithm.md

这个题目就非常试用, 但是我觉得Greedy Algorithm的难点是如何证明它是对的. 这里的思路是每一步都在允许的步数范围内取最大的数, 举个例子:

```
nums = [2, 3, 1, 1, 4]

1. index = 0, value = 2; 此时可以选择的有: index = 1, value = 3 和 index = 2, value = 1; 我们选择最大的3.
2. index = 2, value = 3; 此时可以选择的有: index = 2, value = 1; index = 3, value = 1; index = 4, value 4 = 4; 我们选择4, 此时达到nums的最后一位.

所以最后的结果为2
```

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: for循环遍历了nums数组, n为数组的长度.
* **Space Complexity: O(1)**: 只声明了一些变量.

```java
class Solution 
{
    public int jump(int[] nums) 
    {
        if(nums == null || nums.length == 0)
            return 0;
        
        int currentMaxIndex = 0;
        int nextMaxIndex = 0;
        int steps = 0;
        
        for(int i=0; i<nums.length-1; i++)
        {
            currentMaxIndex = Math.max(i + nums[i], currentMaxIndex);
            if(nextMaxIndex == i)
            {
                steps ++;
                nextMaxIndex = currentMaxIndex;
            }
        }
        
        return steps;
    }
}
```
