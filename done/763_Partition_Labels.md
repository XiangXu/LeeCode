# Partition Labels

A string S of lowercase English letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

Example 1

```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

## First Solution

Use a map to store the largest index for each character in String S.

Runtime: **16 ms**

Memory: **40.8 MB**


```java
class Solution 
{
    public List<Integer> partitionLabels(String S) 
    {
        if(S == null || S.length() == 0)
            return Collections.emptyList();
        
        Map<Character, Integer> maxIndexMap = new HashMap<>();
        for(int i=0; i<S.length(); i++)
            maxIndexMap.put(S.charAt(i), i);
        
        List<Integer> result = new ArrayList<>();
        int start = 0;
        int last = 0;
        for(int i=0; i<S.length(); i++)
        {
            last = Math.max(last, maxIndexMap.get(S.charAt(i)));
            if(i == last)
            {
                result.add(last-start+1);
                start = last+1;
            }
        }
        
        return result;
    }
}
```

**Time Complexity: O(n)**

**Space Complexity: O(n)**

