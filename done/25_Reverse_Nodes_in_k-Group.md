# Reverse Nodes in k-Group

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. 

If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

Example:

```
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
```

Note

* Only constant extra memory is allowed.
* You may not alter the values in the list's nodes, only nodes itself may be changed.


## First Solution

Runtime: **0 ms**

Memory: **39.7 MB**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution 
{
    public ListNode reverseKGroup(ListNode head, int k) 
    {
        if(head == null || head.next == null || k < 2)
            return head;
        
        ListNode current = head;
        int count = 0;
        while(current != null && count < k-1)
        {
            count ++;
            current = current.next;
        }
        
        if(current == null)
            return head;
        
        ListNode next = current.next;
        current.next = null;
        ListNode newList = reverse(head);
        
        head.next = reverseKGroup(next, k);
        
        return newList;
    }
    
    private ListNode reverse(ListNode head)
    {
        ListNode pre = null;
        while(head != null)
        {
            ListNode next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }

        return pre;
    }
}
```

**Time Complexity: O(n)** 

**Space Complexity: O(n)**