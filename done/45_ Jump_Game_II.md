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