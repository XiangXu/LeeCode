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

## Solution

这道题的解题思路如下, 我们用题目中的例子来说明:

```
s = "barfoothefoobarman",
words = ["foo","bar"]
```

1. 首先定义一个Map<String, Integer>, map中的key用来存储words中的word, value则是记录word出现次数,此时hashmap为{foo -> 1, bar -> 1}
2. 然后我们定两个变量: len = words中单个String的长度  totalLen= words中String总长度, 这里len = 3, totalLen = 6.
3. 我们开始遍历String s, 我们每次拿len = 3的substring, 当index = 0的时候, 拿出的为: bar. map是包含这个key-"bar"的, 这个时候i就是一个起点. 我们从index = 0开始拿出长度为totalLen = 6的substring为"barfoo", 然后我们再依次从"barfoo"按照len = 3拿substring, 这样的话就为bar和foo, 每拿出一个我们就看map是否包含, 如果包含count--, 如果不包含或者count == 0 说明当前字符串不满足条件. 当我们能够遍历完"barfoo", 说明当前的"barfoo"满足题意, index = 0 就是一个结果.
4. 如果不包含的话我们向右移动index, 继续重复3.

这道题的思路感觉说起来有点绕但是看代码的话应该比较直观

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 遍历字符串s的for循环, n为s的长度.
* **Space Complexity: O(n))**: 这里用了一个Map来存储word出现的次数, n为map的大小.

```java
class Solution 
{
    public List<Integer> findSubstring(String s, String[] words) 
    {
        if(s == null || s.length() == 0 || words == null || words.length == 0)
            return Collections.emptyList();
        
        int len = words[0].length();
        int totalLen = len * words.length;
        List<Integer> result = new ArrayList<>();
        
        Map<String, Integer> wordsMap = new HashMap<>();
        for(String word : words)
            wordsMap.put(word, wordsMap.getOrDefault(word, 0) + 1);        
        
        for(int i=0; i<=s.length()-totalLen; i++)
        {
            // we need to update count in map so we need a copy of it everytime
            Map<String, Integer> copy = new HashMap<>(wordsMap);
            String tmpWord = s.substring(i, i+len);
            if(copy.containsKey(tmpWord) && isValidSubString(i, len, s.substring(i, i+totalLen), copy))
                result.add(i);
        }
        
        return result;
    }
    
    private boolean isValidSubString(int index, int len, String str, Map<String, Integer> copy)
    {
        int i=0; 
        while(i <= str.length()-len)
        {
            String tmpStr = str.substring(i, i+len);
            if(!copy.containsKey(tmpStr) || copy.get(tmpStr) == 0)
                return false;
            
            int count = copy.get(tmpStr);
            copy.put(tmpStr, --count);
            i+=len;
        }
        
        return true;
    }
}
```