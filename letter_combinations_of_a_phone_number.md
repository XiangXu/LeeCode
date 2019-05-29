# Letter Combinations of a Phone Number

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example:  

Input: "23"  
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]

## First solution
1. Use a hash map to store number and letters.
2. Loop each character in given digits and find out corresponding letter lists.
3. Loop each letter list and append results. 

Runtime: **1 ms**

```java
class Solution 
{
    public List<String> letterCombinations(String digits) 
    {
      
        List<String> result = Collections.emptyList();
       
        if(digits == null || digits.length() == 0 || digits.indexOf("1") >= 0 || digits.indexOf("0") >= 0)
            return result;
        
        Map<Character, List<String>> mapper = generatePhoneNumberLetterMapper();
        result = mapper.get(digits.toCharArray()[0]);
        
        for(int i=1; i<digits.toCharArray().length; i++)
        {
            result = generateCombinations(result, mapper.get(digits.toCharArray()[i]));
        }
        return result;
    }
    
    private List<String> generateCombinations(List<String> result, List<String>currentList)
    {
        List<String> tempResult = new ArrayList();
        for(int i=0; i<result.size(); i++)
        {
            for(int j=0; j<currentList.size(); j++)
            {
                tempResult.add(result.get(i) + currentList.get(j));
            }
        }
        return tempResult;
    }
    
    private Map<Character, List<String>> generatePhoneNumberLetterMapper()
    {
        Map<Character, List<String>> mapper = new HashMap<>();
        mapper.put('2', Arrays.asList("a", "b", "c"));
        mapper.put('3', Arrays.asList("d", "e", "f"));
        mapper.put('4', Arrays.asList("g", "h", "i"));
        mapper.put('5', Arrays.asList("j", "k", "l"));
        mapper.put('6', Arrays.asList("m", "n", "o"));
        mapper.put('7', Arrays.asList("p", "q", "r", "s"));
        mapper.put('8', Arrays.asList("t", "u", "v"));
        mapper.put('9', Arrays.asList("w", "x", "y", "z"));
        return mapper;
    }
}
   
```
