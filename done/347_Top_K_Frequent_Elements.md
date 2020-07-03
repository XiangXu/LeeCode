# Top K Frequent Elements

Given a non-empty array of integers, return the k most frequent elements.

Example 1

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

Example 2

```
Input: nums = [1], k = 1
Output: [1]
```

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
* It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
* You can return the answer in any order.


## First Solution - PriorityQueue

Runtime: **22 ms**

Memory: **47.5 MB**

```java
class Solution
{
    public int[] topKFrequent(int[] nums, int k) 
    {
        int[] result = new int[k];
        
        if(nums == null || nums.length == 0 || nums.length < k)
            return result;
        
        Map<Integer, Integer> countMap = new HashMap<>();
        for(int num : nums)
        {
            countMap.put(num, countMap.getOrDefault(num, 0) + 1);
        }
        
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>(
            (a, b) -> countMap.get(a) - countMap.get(b)
        );
        
        for(int num : countMap.keySet())
        {
            queue.offer(num);
            if(queue.size() > k)
                queue.poll();
        }
        
        for(int i=k-1; i>=0; i--)
        {
            result[i] = queue.poll();
        }
        
        return result;
    }
}
```

**Time Complexity: O(Nlogk)** where N is the length of words. We count the frequency of each word in O(N) time, then we add N words to the queue, each in O(logk) time. Finally we pop from the head up to k times. As k <= N, this is O(Nlogk) in total.

**Space Complexity: O(n)**
