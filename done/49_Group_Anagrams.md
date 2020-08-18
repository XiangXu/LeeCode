# Group Anagrams

Given an array of strings, group anagrams together.

Example:

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

Note:

* All inputs will be in lowercase.
* The order of your output does not matter.

## Solution

这道题还是没能自己想出解法,大概看了一下答案的思路感觉还是挺简单的. 我们可以遍历所给的数组strs, 然后将每个str的字符排序. 创建一个Map, key用来存排序以后相同的str, value用来存储index. 

## 空间时间复杂度分析:

* **Time Complexity: O(NKlogK)**: N是所给字符串长度, K是最长字符串长度, 排序字符串中的字符是KlogK.
* **Space Complexity: O(n)**: 定义的Map.


```java
class Solution 
{
    public List<List<String>> groupAnagrams(String[] strs) 
    {
        if(strs == null || strs.length == 0)
            return Collections.emptyList();
        
        Map<String, List<String>> map = new HashMap<>();  
        
        for(String str : strs)
        {
            char[] charArr = str.toCharArray();
            Arrays.sort(charArr);
            String keyStr = new String(charArr);
            
            if(!map.containsKey(keyStr))
                map.put(keyStr, new ArrayList<>());
            
            map.get(keyStr).add(str);
        }
        
        return new ArrayList<>(map.values());
    }
}
```


