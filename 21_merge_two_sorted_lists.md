# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## First Solution

Runtime: **0 ms**

Memory: **39.1 MB**

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution 
{
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) 
    {        
        ListNode result = new ListNode(0);
        ListNode handler = result;
        
        while(l1 != null && l2 != null)
        {
            if(l1.val <= l2.val)
            {
                handler.next = l1;
                l1 = l1.next;
            }
            else
            {
                handler.next = l2;
                l2 = l2.next;
            }
            handler = handler.next;
        }
        
        if(l1 != null)
            handler.next = l1;
        else if(l2 != null)
            handler.next = l2;
        
        return result.next;
    }
}

```

**Time Complexity: O(n)** 

**Space Complexity: O(n)**

## Second Solution

Runtime: **0 ms**

Memory: **38.8 MB**

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution 
{
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) 
    {        
        if(l1 == null) 
            return l2;
        if(l2 == null) 
            return l1;
        
        ListNode handler;
        if(l1.val< l2.val)
        {
            handler = l1;
            handler.next = mergeTwoLists(l1.next, l2);
        }
        else
        {
            handler = l2;
            handler.next = mergeTwoLists(l1, l2.next);
        }
   
        return handler;
    }
}

```

**Time Complexity: O(n)** 

**Space Complexity: O(n)**
