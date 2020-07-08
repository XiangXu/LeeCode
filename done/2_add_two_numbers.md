# Add Two Numbers - (Medium)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
```

## Solution

一般关于ListNode的题目我觉得要注意两个点:

1. 只要关于ListNode的题目大部分的话需要创建一个dummyHead初始化一个值然后最终的结果为dummyHead.next. 
2. 在遍历所给的ListNode的时候最好也是用一个新的ListNode指向所给的ListNode, 不然的话有可能会改变所给ListNode的值或者结构**.

这道题感觉也没有太大的难度, 解法步骤如下:

1. 同时遍历两个ListNode然后把每个值加起来.
2. 如果两个数的和大于10来的话, 那么当前的值就应该是10取模以后的值, 然后把1传递给下一次计算.
3. 需要注意的是如果最后一位的结果大于10的话需要再加一个1.

## 空间时间复杂度分析:

* **Time Complexity: O(max(m, n))**: m和n表示l1和l2的长度, 所以时间复杂度是遍历两个ListNode中较长的那个所花费的时间.
* **Space Complexity: O(max(m, n))**: m和n表示l1和l2的长度, 最总结果dummyHead最坏的情况是O(max(m, n))+1.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) 
    {
        ListNode dummyHead = new ListNode(0);
        ListNode p = l1, q = l2, curr = dummyHead;
        int carry = 0;
        
        while(p != null || q != null)
        {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            
            int sum = x + y + carry;
            carry = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if( p != null)
                p = p.next;
            if(q != null)
                q = q.next;
        }
        
        if(carry > 0)
            curr.next = new ListNode(carry);
        
        return dummyHead.next;
    }
}
```
