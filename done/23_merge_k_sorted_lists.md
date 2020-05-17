# Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## First Solution

Runtime: **14 ms**

Memory: **45.3 MB**

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

**Time Complexity: O(n<sup>2</sup>)** 

**Space Complexity: O(m+n)**
