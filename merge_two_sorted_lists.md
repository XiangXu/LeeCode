# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4<br>
Output: 1->1->2->3->4->4<br>

## First Solution
1. Insert all integer numbers into an array list.
2. Sort array list
3. Insert integer back into list node. 

Runtime: **3 ms**

```java
class Solution
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
        List<Integer> list = new ArrayList<>();
        addValueIntoList(l1, list);
        addValueIntoList(l2, list);
        Collections.sort(list);
        
        ListNode result = new ListNode(0);
        ListNode currListNode = result;
        
        for(int i=0; i<list.size(); i++)
        {
            ListNode temp = new ListNode(list.get(i));
            currListNode.next = temp;
            currListNode = currListNode.next;
        }
        
        return result.next;
    }
    
    private void addValueIntoList(ListNode l1, List<Integer> list)
    {
        if(list == null || l1 == null)
            return;
        
        list.add(l1.val);
        while(l1.next != null)
        {
            list.add(l1.next.val);
            l1 = l1.next;
        }
    }
}
```

## Second Solution
1. Create a dummy head list node to save the results.
2. Create an handler point to dummy head list node as a pointer.
3. Use a while loop to compare value.

Runtime: **0 ms**

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

## Third Solution
We would use recursion but I think it may cause stack overflow in real life.

Runtime: **0 ms**

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
