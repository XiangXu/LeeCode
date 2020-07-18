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


## Solution

这道题我第一次看到题目是没有做出来的, 看了答案以后有了一些思路, 这道题目我们用到了反转链表, 我其实觉得反转链表挺难理解的, 这里要特别感谢一下这片文章: https://juejin.im/post/5e3d3f25e51d45270c276fe3, 讲解的非常清楚.

我们以所给的第三个例子来说明一下思路:

1->2->3->4->5  k=3

1. 我们可以申明一个curr的指针, 然后将其移动k-1=2位, 这时候curr指向的是3. 
2. 如果此时curr.next不等于null的话, 我们将3的下一位ListNode设为ListNode next = curr.next, 我们接下来要用到这个值.
3. 接下来我们将curr.next = null, 这样做的原因其实就是断开了3->4的这个联系, 此时ListNode被分成来两个部分1->2->3和4->5.
4. 然后我们需要写一个方法来返回一个reverse的ListNode, 将第一部分也就是1->2->3传入, 这时候拿到的ListNode就为3->2->1.
5. 最后我们再次调用当前方法reverseKGroup然后将next传入, 形成一个递归调用, 把剩余的部分也反转, 最后就能得到结果.

这里要格外说明一下下面这段代码:

```java
ListNode newListNode = reverse(head);
head.next = reverseKGroup(next, k);
```

我在第二次做的时候又犯了一个错误, 我直接是写成newListNode.next = reverseKGroup(next, k), 这样的答案返回的就是4->5.

这里要用head.next的原因是, newListNode的值其实每一次都会被改写: 3->2->1和4->5. 为什么head.next以后结果就正确来呢? 

那么我们来看一下reverse这个方法, 这个方法其实很简单, 就是用来反转数组. 但是我们要注意, 这里的head传入的其实相当于一个curr的指针, 这样的话第一次调用reverse以后我们得到newListNode = 3->2->1, 此时head指向的是1, 那么head.next其实就是将newListNode中的1指向了next这一下半部分也就是4->5, 这样就得到了最终的结果.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是所给head的长度, 这里我们遍历了一遍ListNode.
* **Space Complexity: O(1)**: 我们只声明了一些变量.

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
        if(head == null || head.next == null)
            return head;
        
        ListNode curr = head;
        int count = 0;
        
        while(curr != null && count < k-1)
        {
            curr = curr.next;
            count++;
        }

        if(curr == null)
            return head;
        
        ListNode next = curr.next;
        curr.next = null;
        
        ListNode newListNode = reverse(head);
        head.next = reverseKGroup(next, k);
        
        return newListNode;   
    }
    
    private ListNode reverse(ListNode curr)
    {
        ListNode prev = null;
        while(curr != null)
        {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```







