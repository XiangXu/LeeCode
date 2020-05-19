# Swap Nodes in Paris

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example:

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

## First Solution

Runtime: **0 ms**

Memory: **38.9 MB**

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
    public ListNode swapPairs(ListNode head) 
    {
        if(head == null || head.next == null)
            return head;
        
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode current = dummyHead;
        
        while(current.next != null && current.next.next != null)
        {
            ListNode first = current.next;
            ListNode second = current.next.next;
            
            current.next = second; 
            // 在把第二个和第三个node换位置的时候需要将第二个的node和第四个node连接起来     
            first.next = second.next;
            current.next.next = first;
            
            current = current.next.next;
        }
        
        return dummyHead.next;
    }
}
```

**Time Complexity: O(n)** 

**Space Complexity: O(l)**