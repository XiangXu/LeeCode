# Top K Frequent Words

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

Example 1

```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words. Note that "i" comes before "love" due to a lower alphabetical order.
```

Example 2

```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
```

## First Solution - PriorityQueue

Runtime: **5 ms**

Memory: **39.7 MB**

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) 
    {
        if(words == null || words.length ==0 || words.length < k)
            return Collections.emptyList();
        
        Map<String, Integer> countMap = new HashMap<>();
        
        for(String word : words)
        {
            countMap.put(word, countMap.getOrDefault(word, 0) + 1);
        }
        
        PriorityQueue<String> queue = new PriorityQueue<String>(
            (a, b) -> countMap.get(a) == countMap.get(b) ? b.compareTo(a) : countMap.get(a) - countMap.get(b)
        );
        
        for(String word : countMap.keySet())
        {
            queue.offer(word);
            if(queue.size() > k)
                queue.poll();
        }
        
        List<String> result = new ArrayList<>();
      
        while(!queue.isEmpty())
            result.add(queue.poll());
       
        Collections.reverse(result);
        
        return result;
            
    }
}
```

**Time Complexity: O(Nlogk)** where N is the length of words. We count the frequency of each word in O(N) time, then we add N words to the queue, each in O(logk) time. Finally we pop from the head up to k times. As k <= N, this is O(Nlogk) in total.

**Space Complexity: O(n)**

