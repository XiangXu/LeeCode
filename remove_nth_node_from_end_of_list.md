# Remove Nth Node From End of List

Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.


## First Solution
1. Get the length of given list node.
2. Find the index and unlink it from the given list 


Runtime: **782 ms**

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
        int length = 0;
        ListNode result = new ListNode(0);
        result.next = head;
        ListNode first = head;
        
        while(first != null)
        {
            length += 1;
            first = first.next;
        }
        
        length -= n;
        first = result;

        while(length > 0)
        {
            length--;
            first = first.next;
        }
        
        first.next = first.next.next;
        
        return result.next;
    }
}

```
