# Merge Intervals

Given a collection of intervals, merge all overlapping intervals

Example 1:

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

Example 2:

```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

## First Solution

Runtime: **11 ms**

Memory: **44.8MB**

```java
class Solution 
{
    public int[][] merge(int[][] intervals)
    {
        if(intervals == null || intervals.length <= 1)
            return intervals;
        
        Arrays.sort(intervals, (arr1, arr2) -> arr1[0] - arr2[0]);
        
        List<int[]> list = new ArrayList<>();
        int[] currentInterval = intervals[0];
        list.add(currentInterval);
        
        for(int i=1; i<intervals.length; i++)
        {
            int currentBegin = currentInterval[0];
            int currentEnd = currentInterval[1];
            
            int nextBegin = intervals[i][0];
            int nextEnd = intervals[i][1];
            
            if(currentEnd >= nextBegin)
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            else
            {
                currentInterval = intervals[i];
                list.add(currentInterval);
            }
        }
        
        int[][] result = new int[list.size()][2];
        for(int i=0; i < list.size(); i++)
            result[i] = list.get(i);
        
        return result;
    }
}
```

**Time Complexity: O(nlog(n))**

**Space Complexity: O(n)**
    