# Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.   
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


## First Solution - Brute Force

Check all the substring one by one to see if it has no duplicate character.

Runtime: **Time Limit Exceeded**  
Memory: **N/A**

```java
class Solution 
{
    public int lengthOfLongestSubstring(String s) 
    {
        int n = s.length();
        int result = 0;
        for(int i = 0; i < n; i++)
        {
            for(int j = i + 1; j <= n; j++)
            {
                if(allUnique(s, i, j))
                    result = Math.max(result, j - i);
            }
        }
        return result;
    }
    
    private boolean allUnique(String s, int start, int end)
    {
        Set<Character> set = new HashSet<>();
        for(int i = start; i < end; i++)
        {
            Character ch = s.charAt(i);
            if(set.contains(ch))
                return false;
            set.add(ch);
        }
        
        return true;
    }
}
```

### Complexity Analysis

**Time Complexity: O(n^3)** 

**Space Complexity: O(min(n,m))**

We need O(k) space for checking a substring has no duplicate characters, where k is the size of the Set. The size of the Set is upper bounded by the size of the string nn and the size of the charset/alphabet mm.


## Second Solution - Sliding Window

A sliding window is an abstract concept commonly used in array/string problems.   
A window is a range of elements in the array/string which usually defined by the start and end indices, i.e. [i, j)[i,j) (left-closed, right-open).   
A sliding window is a window "slides" its two boundaries to the certain direction. For example, if we slide [i, j)[i,j) to the right by 11 element, then it becomes [i+1, j+1)[i+1,j+1) (left-closed, right-open).

Runtime: **8 ms**  
Memory: **41.6 MB**

```java
class Solution 
{
    public int lengthOfLongestSubstring(String s) 
    {
        int n = s.length();
        int ans = 0, i = 0, j = 0;
        
        Set<Character> set = new HashSet<>();
        
        while(i < n && j < n)
        {
            if(!set.contains(s.charAt(j)))
            {
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            }
            else
            {
                set.remove(s.charAt(i++));
            }
        }
        
        return ans; 
    }
}
```

**Time Complexity: O(n)** 

Time complexity : O(2n)=O(n). In the worst case each character will be visited twice by i and j.

**Space Complexity: O(min(n,m))**

O(min(m,n)). Same as the previous approach. We need O(k) space for the sliding window, where k is the size of the Set. The size of the Set is upper bounded by the size of the string n and the size of the charset/alphabet m.


## Third Solution - Sliding Window Optimized
The above solution requires at most 2n steps. In fact, it could be optimized to require only n steps. Instead of using a set to tell if a character exists or not, we could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character.


Runtime: **747 ms**  
Memory: **42.7 MB**

```java
class Solution 
{
    public int lengthOfLongestSubstring(String s) 
    {
        int n = s.length();
        int ans = 0;
        
        Map<Character, Integer> map = new HashMap<>();
        
        for(int i=0, j=0; j<n; j++)
        {
            if(map.containsKey(s.charAt(j)))
            {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j-i+1);
            map.put(s.charAt(j), j+1);
        }
        
        return ans;
    }
}
```

**Time Complexity: O(n)** 

**Space Complexity: O(min(n,m))**
