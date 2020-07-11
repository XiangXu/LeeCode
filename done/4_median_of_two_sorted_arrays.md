# Median of Two Sorted Arrays - (Hard)

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Solution

这是我在leetcode上碰见的第一道hard难度的题, 我当时的第一想法就是讲这两个数组中的数字插入到一个数组中, 然后按照从小到达的顺序重新排列这个数组，然后找到中间的一个或者两个数求平均数. 很显然这道题目不能这样做, 因为题目中要求空间复杂度必须是O(log(m+n)). 

**一般来说看到时间复杂度为log(n)我们肯定就要使用binary search了**.

下面来说一下这道题目的解题思路:

答案里所给的两个数组太小了，假设我们有下面两个数组:

nums1: 2   4   6  |  9   10   

nums2: 1   3   5  |  7   11   13   16

total: 1   2   3   4   5   6  ｜  7   9   10   11   13   16

对于上面所给的两个数组呢, 中位数就应该是: (6 + 7) / 2 = 6.5. 那么我们应该如何找到这个6和7呢？

这里有一个规律, 因为这两个数组都是从小到大排好序的，我们可以这样来找:

首先呢, 我们先看total, 我们知道最终的结果是6和7, 如果我们将6和7的中间切一刀, 那么切点左边和右边将会分别由部分num1和部分num2来组成, 各为6个数字.

```            L1    R1
nums1: 2   4   6  |  9   10  

               L2    R2
nums2: 1   3   5  |  7   11   13   16


total: 1   2   3   4   5   6  ｜  7   9   10   11   13   16
```
这时候呢, 我们知道6是在total分割线的左边, 7是在分割线的右边. 那么我们在nums1中, 将分割线如上图所示定在6的后面, 此时左边已经有了3个元素, 那么我就知道了nums2需要提供3个元素, 所以呢nums2的分割线就应该化在5的后面.

在知道了以上的信息的情况下, 我们的问题就变成了如何找到nums1的分割线, 这样我们就将复杂的问题给简单化了.

那么我们怎么来找到这个nums1的分割线呢, 这时候我们要注意到一个规律:

因为这两个数组都是排序的数组, 所以我们来看一下L1,R1和L2,R2这四个值的特点, 当达成上述条件的时候 **L1的值应该小于R2的值, L2的值需要小于R1**.

如果R1的值小于L2说明我们的在nums1的切点太小要向后移. 如果L1的值大于R2的值则说明我们在nums1的切点太大要向前移.

如何来定这个切点呢. 我们可以使用binary search.

## 空间时间复杂度分析:

* **Time Complexity: O(log(min(m,n)))**: m和n表示nums1和num2的长度, 我们用了binarySearch在较短的数组中查找切点.
* **Space Complexity: O(1)**: 我们只是存了一些变量的值.

```java
class Solution 
{
    public double findMedianSortedArrays(int[] nums1, int[] nums2)
    {
        int len1 = nums1.length;
        int len2 = nums2.length;
        
        if(len1 > len2)
            return findMedianSortedArrays(nums2, nums1);
        
        if(len1 == 0)
        {
            if(len2 % 2 == 0)
                return (double)((nums2[len2/2-1] + nums2[len2/2])) / 2;
            else
                return (double)nums2[len2/2];
        }
        
        int len = len1 + len2;
        // cut1 and cut2 are used to show how many numbers on the left side of the cut point
        int cut1 = 0;
        int cut2 = 0;
        int start = 0;
        int end = len1;
        
        while(start <= end)
        {
            cut1 = start + (end - start) / 2;
            cut2 = len / 2 - cut1;
            
            int L1 = (cut1 == 0) ? Integer.MIN_VALUE : nums1[cut1-1];
            int L2 = (cut2 == 0) ? Integer.MIN_VALUE : nums2[cut2-1];
            int R1 = (cut1 == len1) ? Integer.MAX_VALUE : nums1[cut1];
            int R2 = (cut2 == len2) ? Integer.MAX_VALUE : nums2[cut2];
            
            if(R1 < L2)
                start = cut1 + 1;
            else if(L1 > R2)
                end = cut1 - 1;
            else
            {
                if(len % 2 == 0)
                    return (double)(Math.max(L1, L2) + Math.min(R1, R2)) / 2;
                else
                    return (double)(Math.min(R1, R2));
            }
        }
        
        return 0.0;
            
    }
}
```