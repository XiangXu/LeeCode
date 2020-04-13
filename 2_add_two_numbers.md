# Add Two Numbers

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

## First Solution

1. Initialize current node to dummy head of the returning list.
2. Initialize carry to 00.
3. Initialize pp and qq to head of l1l1 and l2l2 respectively.
4. Loop through lists l1l1 and l2l2 until you reach both ends.
   Set xx to node pp's value. If pp has reached the end of l1l1, set to 00.
   Set yy to node qq's value. If qq has reached the end of l2l2, set to 00.
   Set sum = x + y + carrysum=x+y+carry.
   Update carry = sum / 10carry=sum/10.
   Create a new node with the digit value of (sum \bmod 10)(summod10) and set it to current node's next, then advance current node to next.
   Advance both pp and qq.
5. Check if carry = 1carry=1, if so append a new node with digit 11 to the returning list.
6. Return dummy head's next node.
 
Runtime: **2 ms**  
Memory: **41.4 MB**

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
### Complexity Analysis

**Time complexity : O(max(m, n))**  

Assume that m and n represents the length of l1 and l2 respectively, the algorithm above iterates at most max(m,n) times.

**Space complexity : O(max(m,n))** 

The length of the new list is at most max(m,n)+1.
