# Remove Nth Node From End of List

Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.


## First Solution
Fast Slow Pointers
dummyHead->1->2->3->4->5
                 f
           s
                       f
                 s

Runtime: **0 ms**

Memory: **38 MB**

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
    public ListNode removeNthFromEnd(ListNode head, int n) 
    {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode fast = dummyHead;
        ListNode slow = dummyHead;
        
        for(int i=0; i<=n; i++)
        {
            fast = fast.next;
        }
        
        while(fast != null)
        {
            fast = fast.next;
            slow = slow.next;
        }
        
        slow.next = slow.next.next;
        
        return dummyHead.next;
    }
}
```

**Time Complexity: O(n)** 

**Space Complexity: O(1)**
