# Next Permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

## Solution

这道题要求我们置换位置来得到下一个较大的排列数字, 想了很久没有找到规律, 看了答案以后一目了然,这道题目感觉就是考思路.

下面我们通过一个例子来看一下具体的解法:
1. Input: [1,2,5,7,11,6,4,3] Result: [1,2,5,11,3,4,6,7].
3. 我们首先从右往左遍历数组, 找到第一个数字开始变小的index, 这里这个数字是7而index是3.
4. 如果没有找到说明这个数组是从右到左依次变大的, 这个时候我们直接反转数组就能得到结果.
5. 然后我们再从右到找到第一个数字比7大的index, 这里这个数组是11而index是4.
6. 我们将7和11交换位置得到:[1,2,5,11,7,6,4,3]
7. 最后我们从7开始将数组从小到达排序得到: [1,2,5,11,3,4,6,7], 这就是最终的答案.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 从右到左遍历nums数组的循环, n为nums的长度.
* **Space Complexity: O(1))**: 这里只声明了一些变量.


```java
class Solution 
{
    public void nextPermutation(int[] nums) 
    {
        if(nums == null || nums.length == 0 || nums.length == 1)
            return;
        
        int len = nums.length;
        
        int firstSmallerIndex = -1;
        for(int i=len-2; i>=0; i--)
        {
            if(nums[i+1] > nums[i])
            {
                firstSmallerIndex = i;
                break;
            }
        }
        
        if(firstSmallerIndex == -1)
        {
            reverse(nums, 0, len-1);
            return;
        }
            
        
        int firstLargerIndex = -1;
        for(int i=len-1; i>=0; i--)
        {
            if(nums[i] > nums[firstSmallerIndex])
            {
                firstLargerIndex = i;
                break;
            }
        }
        
        swap(firstSmallerIndex, firstLargerIndex, nums);
        reverse(nums, firstSmallerIndex+1, len-1);
    }
    
    private void reverse(int[] nums, int i, int j)
    {
        while(i < j)
        {
            swap(i, j, nums);
            i++;
            j--;
        }
    }
    
    private void swap(int i, int j, int[] nums)
    {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

