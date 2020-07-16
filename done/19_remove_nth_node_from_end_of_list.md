# Remove Nth Node From End of List

Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.

Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?


## Solution

我们之前说过, 一般看到ListNode的题目的话, 我们就需要创建一个dummyHead, 这题也不例外. 这道题其实有两种解法, 我刚拿到这道题目的时候只知道第一种, 下面我们来分别说一下这两种解法.

第一种解法其实特别的简单粗暴, 我们遍历所有的ListNode, 这样我们就可以拿到整个ListNode的总长度， 举个例子:

1->2->3->4->5, and n = 2, len = 5;

4其实倒数第二位但是其实也是正数的第三位5-2=3, 知道了这个3的index以后我们再遍历数组到第三位然后去掉下一位的4就可以了. 具体代码如下:

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里我们遍历了所给的ListNode, n为ListNode的长度.
* **Space Complexity: O(1)**: 这里我们只声明了一些变量.
 
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
    public ListNode removeNthFromEnd(ListNode head, int n) 
    {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        
        ListNode curr = head;
        int len = 0;
        
        while(curr != null)
        {
            len ++;
            curr = curr.next;
        }
        
        len -= n;
        curr = dummyHead;
        
        while(len > 0)
        {
            len --;
            curr = curr.next;
        }
        
        curr.next = curr.next.next;
        
        return dummyHead.next;
    }
}
```

第二个解法是**快慢指针**, 我在第二次做这道题的时候已经掌握了这个方法, 其实感觉还是挺巧妙的, 下面我们来解释一下什么叫快慢指针:

假设我们还是下面这个例子:

1->2->3->4->5, and n = 2;

1. 我们取两个指针left, right都指向1.
2. 开始的时候我们先将right向前移动n=2位， 这个时候right就会指向3, 而left仍然指向的1.
3. 接下来我们开始同时移动两个指针, 当right到达5的时候, left就会指向3.
4. 最后我们将left的下一位指向它的下下一位这样就完成了题目的要求.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: 这里我们遍历了所给的ListNode, n为ListNode的长度.
* **Space Complexity: O(1)**: 这里我们只声明了一些变量.
 

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
    public ListNode removeNthFromEnd(ListNode head, int n) 
    {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        
        ListNode slow = dummyHead;
        ListNode fast = dummyHead;
        
        while(n >= 0)
        {
            fast = fast.next;
            n --;
        }
        
        while(fast != null)
        {
            fast = fast.next;
            slow = slow.next;
        }
        
        slow.next = slow.next.next;
        
        return dummyHead.next;
    }
}
```
