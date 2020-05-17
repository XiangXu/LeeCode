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

When we see log(m+n), we know we need to use **Binay Search**.

nums3: 1   2   3   5   7   8   9   11   12
	       
nums1: 3   5   8   9   14
               
nums2: 1   2   7   10  11   12

The four elements must obtain

L1 <= R2

L2 <= R1

if L1 > R2, end = cut1 - 1;

if L2 > R1, start = cut1 + 1;

cut1: the number of elements on left side of cut point in nums1

cut2: the number of elements on left side of cut point in nums2.

Runtime: **12 ms**  
Memory: **46.1 MB**

```java
class Solution 
{
    public double findMedianSortedArrays(int[] nums1, int[] nums2) 
    {
        int length1 = nums1.length;
        int length2 = nums2.length;
        if(length1 > length2)
            return findMedianSortedArrays(nums2, nums1);
        
        if(length1 == 0)
            return ( (double)(nums2[(length2 - 1) / 2]) + (double)nums2[length2 / 2] )/2;
        
        int length = length1 + length2;
        int cut1 = 0;
        int cut2 = 0;
        int cutL = 0;
        int cutR = length1;
        
        while(cutL <= cutR)
        {
            cut1 = (cutL + cutR) / 2;
            cut2 = length / 2 - cut1;
            
            double L1 = (cut1 == 0) ? Integer.MIN_VALUE : nums1[cut1 - 1];
            double L2 = (cut2 == 0) ? Integer.MIN_VALUE : nums2[cut2 - 1];
            double R1 = (cut1 == length1) ? Integer.MAX_VALUE : nums1[cut1];
            double R2 = (cut2 == length2) ? Integer.MAX_VALUE : nums2[cut2];
            
            if(L1 > R2)
                cutR = cut1 - 1;
            else if(L2 > R1)
                cutL = cut1 + 1;
            else
            {
                if(length % 2 == 0)
                    return (Math.max(L1,L2) + Math.min(R1,R2)) / 2;
                else
                    return Math.min(R1, R2);
            }
        }
        
        return 0.0;
    }
}
```

**Time Complexity: O(log (m+n)).** 

**Space Complexity: O(l)**
