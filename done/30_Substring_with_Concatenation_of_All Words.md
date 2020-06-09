# Substring with Concatenation of All Words

You are given a string, s, and a list of words, words, that are all of the same length. 

Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

Example 1:

```
Input:
  s = "barfoothefoobarman",
  words = ["foo","bar"]
Output: [0,9]

Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```

Example 2:

```
Input:
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
Output: []
```

## First Solution

Use HashMap to handle intervening characters.

Runtime: **319 ms**

Memory: **115.1 MB**

```java
class Solution 
{
    public List<Integer> findSubstring(String s, String[] words) 
    {
        if(s == null || words == null || s.length() == 0 || words.length == 0)
            return Collections.emptyList();
        
        List<Integer> result = new ArrayList<>();
        int wordsArrLen = words.length;
        int wordLen = words[0].length();
        
        Map<String, Integer> wordsMap = new HashMap<>();
        for(String str : words)
            wordsMap.put(str, wordsMap.getOrDefault(str, 0) + 1);
        
        for(int i=0; i<=s.length()-wordsArrLen*wordLen; i++)
        {
            Map<String, Integer> copy = new HashMap<>(wordsMap);
            int wordCounter = wordsArrLen;
            int index = i;
            while(wordCounter > 0)
            {
                String str = s.substring(index, index+wordLen);
                if(!copy.containsKey(str) || copy.get(str) < 1)
                    break;
                
                copy.put(str, copy.get(str)-1);
                wordCounter --;
                index += wordLen;
            }
            
            if(wordCounter == 0)
                result.add(i);
        }
        
        return result;
    }
}
```

**Time Complexity: O(n<sup>2</sup>)** 

**Space Complexity: O(n))**