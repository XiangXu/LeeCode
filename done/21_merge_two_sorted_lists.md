# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

##  Solution

这题其实还是挺简单的, 没有花费太多的时间, 我写出了第一种方法, 看了答案以后发现其实还是可以用递归来做, 也挺容易理解的.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里n是指l1和l2中较长的那一个ListNode.
* **Space Complexity: O(n)**: 这里我们只声明了一个dummyHead.


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
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2)
    {
        ListNode dummyHead = new ListNode(0);
        ListNode curr = dummyHead;
        
        while(l1 != null || l2 != null)
        {
            int val1 = (l1 == null) ? Integer.MAX_VALUE : l1.val;
            int val2 = (l2 == null) ? Integer.MAX_VALUE : l2.val;
            
            if(val1 < val2)
            {
                curr.next =new ListNode(val1);
                l1 = l1.next;
            }
            else
            {
                curr.next =new ListNode(val2);
                l2 = l2.next;
            }
            
            curr = curr.next;
        }
        
        return dummyHead.next;
    }
}

```

递归的解法, 稍微看一下应该不难理解

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里n是指l1和l2中较长的那一个ListNode.
* **Space Complexity: O(1)**: 这里是直接在修改两个ListNodes.

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

**Space Complexity: O(1)**
