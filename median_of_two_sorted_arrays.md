# Median of Two Sorted Arrays

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:

nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

## First Solution

Actually this solution doesn't meet the requirement because run time complexity should be O(log (m+n)).

We added two array together and sorted them then find the median. 

Runtime: **35 ms**

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
         double result = 0;
		  
		  List<Integer> numList = new ArrayList<>();
		  
		  for (int num1 : nums1) {
			  numList.add(num1);
		  }
		  
		  for (int num2 : nums2) {
			  numList.add(num2);
		  }
		  
		  Collections.sort(numList, new Comparator<Integer>() {
			  @Override
			  public int compare(Integer o1, Integer o2) {
				return o1-o2;
			  }
		  });
		  
		  
		  if(numList.size() % 2 == 0)
		  {
			  int index = numList.size() / 2 - 1;
			  result = Double.valueOf((numList.get(index) + numList.get(index + 1))) / 2;
		  }
		  else
		  {
			  int index = numList.size() / 2;
			  result = Double.valueOf(numList.get(index));
		  }
		 
		  return result;
    }
}
```
