# Reverse Linked List

Reverse a singly linked list.

Example:

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up**:

A linked list can be reversed either iteratively or recursively. Could you implement both?

## First solution

Iterative

Runtime: **0 ms**

Memory: **39 MB**

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
    public ListNode reverseList(ListNode head) 
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

**Time Complexity: O(n>**

**Space Complexity: O(1)**

## Second Solution

Recursive

![img1](/images/reverse_linkedlist_1.png)

![img2](/images/reverse_linkedlist_2.png)

![img3](/images/reverse_linkedlist_3.png)

![img4](/images/reverse_linkedlist_4.png)

![img5](/images/reverse_linkedlist_5.png)

Runtime: **0 ms**

Memory: **39.5 MB**

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
    public ListNode reverseList(ListNode head) 
    {
        if (head == null || head.next == null) 
           return head;
        
        ListNode last = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return last;
    }
}
```

**Time Complexity: O(n)**

**Space Complexity: O(1)**

The extra space comes from implicit stack space due to recursion. The recursion could go up to nn levels deep.

Reference:

https://zhuanlan.zhihu.com/p/86745433?utm_source=wechat_session&utm_medium=social&utm_oi=545451856571195392&from=singlemessage&isappinstalled=0



