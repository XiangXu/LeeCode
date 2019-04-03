# Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

## First Solution
Iterate all characters in that String 
 
Runtime: **2633 ms**

```java
class Solution 
{
    public String longestPalindrome(String s) 
    {
        String result = "";
        
        if(s != null && s.length() > 0)
        {
            for(int i=0; i<s.length(); i++)
            {
                for(int j=i+1; j<=s.length(); j++)
                {
                    String tempStr = s.substring(i, j);
                    if(isPalindromicString(tempStr) && result.length() < tempStr.length()) 
                    {
                        result = tempStr;
                    }
                }
            }
        }
        
        return result;
    }
    
    private boolean isPalindromicString(String s)
    {
        boolean result = false;
        if(s != null && s.length() > 0)
        {
            int left = 0;
            int right = s.length() - 1;
            
            while(left < right)
            {
                if(s.charAt(left) != s.charAt(right))
                {
                    return false;
                }

                left++;
                right--;
            }
        }
        return true;
    }
}
```

## Second Solution
Instead of interating all characters, we put them into a hashmap. In this hashmap, key is each character and value is arraylist which contains all the indexes of each character in the given string. 

Loop all the indexes in each arraylist and get substring between each two indexes then check if that substring is longest palindrome or not. 
 
Runtime: **195 ms**

```java
class Solution 
{
    public String longestPalindrome(String s) 
    {
        String result = "";
        
        if(s != null && s.length() > 0)
        {
            result = Character.toString(s.charAt(0));
            
            Map<Character, List<Integer>> charIndexes = new HashMap<>();
            
            for(int i=0; i<s.length(); i++)
            {
                if(!charIndexes.containsKey(s.charAt(i)))
                {
                    List<Integer> indexes = new ArrayList<>();
                    indexes.add(i);
                    charIndexes.put(s.charAt(i), indexes);
                }
                else
                {
                    List<Integer> indexes = charIndexes.get(s.charAt(i));
                    indexes.add(i);
                }
            }
            
             // System.out.println(charIndexes);
            
            for(List<Integer> indexes: charIndexes.values())
            {
                int currentMaxLength = indexes.get(indexes.size()-1) - indexes.get(0) + 1;
                
                if(result.length() >= currentMaxLength)
                    continue;
                
                for(int i=0; i<indexes.size(); i++)
                {
                    
                    for(int j=indexes.size()-1; j>i; j--)
                    {
                        
                        int indexA= indexes.get(i);
                        int indexB = indexes.get(j)+1;
                        int currentLength = indexB - indexA + 1;
                        
                        // No point to keep going if rest sub string length is less than current result length 
                        if(result.length() >= currentMaxLength)
                            break;

                        String subStr = s.substring(indexA, indexB);
                        
                        //Check length first because isPalindromicString method is slow
                        if(subStr.length() > result.length() && isPalindromicString(subStr))
                            result = subStr;
                    }
                }
            }
            
            
        }
        
        return result;
    }
    
    private boolean isPalindromicString(String s)
    {
        boolean result = false;
        if(s != null && s.length() > 0)
        {
            int left = 0;
            int right = s.length() - 1;
            
            while(left < right)
            {
                if(s.charAt(left) != s.charAt(right))
                {
                    return false;
                }

                left++;
                right--;
            }
        }
        return true;
    }
}
```





