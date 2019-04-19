# Integer to roman
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.  

Symbol       Value  
I             1  
V             5  
X             10  
L             50  
C             100  
D             500  
M             1000  
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.  

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:  

I can be placed before V (5) and X (10) to make 4 and 9.   
X can be placed before L (50) and C (100) to make 40 and 90.   
C can be placed before D (500) and M (1000) to make 400 and 900.  
Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.  

Example 1:

Input: 3
Output: "III"

Example 2:

Input: 4
Output: "IV"

Example 3:

Input: 9
Output: "IX"

Example 4:

Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.

Example 5:

Input: 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
## First Solution
Use a hashmap to store Roman numbers and integers

Runtime: **10 ms**

```java
class Solution 
{
    public String intToRoman(int num) 
    {
        StringBuilder sb = new StringBuilder();
        if(num >= 1 && num <= 3999)
        {
            Map<Integer, String> romanIntMapper = setupIntegerToRomanMapper();
            
            if(num >= 1000)
            {
                int keyValue = num / 1000 * 1000;
                sb.append(romanIntMapper.get(keyValue));
                num = num - keyValue;
            }
        
           if(num >= 100)
           {
               int keyValue = num / 100 * 100;
               sb.append(romanIntMapper.get(keyValue));
                num = num - keyValue;
           }
            
           if(num >= 10)
           {
               int keyValue = num / 10 * 10;
               sb.append(romanIntMapper.get(keyValue));
                num = num - keyValue;
           }
            
           if(num > 0)
           {
               int keyValue = num % 10;
               sb.append(romanIntMapper.get(keyValue));
               num = num - keyValue;
           }
            
        }

        return sb.toString();
        
    }
    
    private Map<Integer, String> setupIntegerToRomanMapper()
    {
        Map<Integer, String> romanIntMapper = new HashMap<>();
       
        romanIntMapper.put(1,    "I");
        romanIntMapper.put(2,    "II");
        romanIntMapper.put(3,    "III");
        romanIntMapper.put(4,    "IV");
        romanIntMapper.put(5,    "V");
        romanIntMapper.put(6,    "VI");
        romanIntMapper.put(7,    "VII");
        romanIntMapper.put(8,    "VIII");
        romanIntMapper.put(9,    "IX");
        romanIntMapper.put(10,   "X");
        romanIntMapper.put(20,   "XX");
        romanIntMapper.put(30,   "XXX");
        romanIntMapper.put(40,   "XL");
        romanIntMapper.put(50,   "L");
        romanIntMapper.put(60,   "LX");
        romanIntMapper.put(70,   "LXX");
        romanIntMapper.put(80,   "LXXX");
        romanIntMapper.put(90,   "XC");
        romanIntMapper.put(100,  "C");
        romanIntMapper.put(200,  "CC");
        romanIntMapper.put(300,  "CCC");
        romanIntMapper.put(400,  "CD");
        romanIntMapper.put(500,  "D");
        romanIntMapper.put(600,  "DC");
        romanIntMapper.put(700,  "DCC");
        romanIntMapper.put(800,  "DCCC");
        romanIntMapper.put(900,  "CM");
        romanIntMapper.put(1000, "M");
        romanIntMapper.put(2000, "MM");
        romanIntMapper.put(3000, "MMM");
        
        return romanIntMapper;
    }
}
```

## Second Solution
Use for arrays to represet:
1000, 2000, 3000
100, 200, 300, 400, 500, 600, 700, 800, 900
10, 20, 30, 40, 50, 60, 70, 80, 90
1, 2, 3, 4, 5, 6, 7, 8, 9

Runtime: **4 ms**
```java
    public String intToRoman(int num) 
    {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
    }
```
