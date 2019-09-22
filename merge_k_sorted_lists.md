# Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:<br>

Input:<br>
[<br>
  1->4->5,<br>
  1->3->4,<br>
  2->6<br>
]<br>
Output: 1->1->2->3->4->4->5->6<br>

## First Solution
1. Iterator all lists and add values into a list
2. Sorted a list 
3. Inert all values from list into a new list node.

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
class Solution 
{
    public ListNode mergeKLists(ListNode[] lists) 
    {
        ListNode result = new ListNode(0);
        ListNode current = result;        
        List<Integer> list = new ArrayList<>();   
        
        for(ListNode listNode: lists)
        {
            while(listNode != null)
            {
                list.add(listNode.val);
                listNode = listNode.next;
            }
        }
        
        Collections.sort(list);
        
        for(int i: list)
        {
            current.next = new ListNode(i);
            current = current.next;
        }
        
        return result.next;
    }
}

```
