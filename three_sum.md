# 3Sum

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]

## First Solution
1. Sort the given array first.
2. Create two lists to store positive(include 0) and negative numbers.
3. Create two maps to store positive(include 0) and negative numers.
4. Check if given array contains more than three zero. If so, add [0,0,0] into result.
5. Loop postivie and negative lists seperately and use two map's key to check if these three numbers' sum is zero.
6. If these three number's sum is zero, then convert them into a string and check if trackMapper contains that string or not.
   trackMpeer is used to avoid duplicate triplets.


Runtime: **782 ms**

```java
class Solution
{
    public List<List<Integer>> threeSum(int[] nums)
    {
        List<List<Integer>> results = new ArrayList<>();

        if(nums ==null || nums.length < 3)
            return results;

        Arrays.sort(nums);

        List<Integer> positiveList = new ArrayList<>();
        List<Integer> negativeList = new ArrayList<>();

        Map<Integer, Integer> positiveMapper = new HashMap<>();
        Map<Integer, Integer> negativeMapper = new HashMap<>();
        Map<String, String> trackMapper = new HashMap<>();

        int zeroCount = 0;
        for(int i: nums)
        {
            if(i >= 0)
            {
                if(i == 0)
                    zeroCount++;
                positiveList.add(i);
                positiveMapper.put(i,null);
            }
            else
            {
                negativeList.add(i);
                negativeMapper.put(i,null);
            }
        }

        findUniqueTriples(positiveList, negativeMapper, trackMapper, results);
        findUniqueTriples(negativeList, positiveMapper, trackMapper, results);

        if(zeroCount >= 3)
        {
            List<Integer >tempList = new ArrayList<>();
            tempList.add(0);
            tempList.add(0);
            tempList.add(0);
            results.add(tempList);
        }

        return results;
    }

    private void findUniqueTriples(List<Integer> list,
                              Map<Integer, Integer>map,
                              Map<String, String>trackMapper,
                              List<List<Integer>> results)
    {
        for(int i=0; i<list.size(); i++)
        {
            for(int j=i+1; j<list.size(); j++)
            {
                int first = list.get(i);
                int second = list.get(j);
                int sum = -first-second;

                int[]tempArr = {first, second, sum};
                Arrays.sort(tempArr);
                List<Integer> tempList = new ArrayList<>();

                String key = "";
                for(int temp: tempArr)
                {
                    tempList.add(temp);
                    key += temp;
                }

                if(map.containsKey(sum))
                {
                    if(trackMapper.containsKey(key))
                        continue;
                    else
                    {
                        trackMapper.put(key, null);
                        results.add(tempList);
                    }
                }
            }
        }
    }
}
```
