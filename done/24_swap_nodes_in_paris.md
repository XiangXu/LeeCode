# Swap Nodes in Paris

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example:

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

## Solution

这道题其实我觉得难度不是很高, 按照正常逻辑的步骤来做的话其实思路很清晰:

1. 首先我们创建一个DummyHead, 初始化为0, 然后将它的下一个ListNode指向head, 最后再声明一个ListNode curr来指向dummyHead.
2. 我们需要确保curr.next和curr.next.next都不为空, 这样我们才可以进行替换.

接下来我们用一个例子来说明, 这样更加直观:

1. dummyHead: 0->1->2->3->4, 此时curr=0;
2. 此时我们声明一个first和second, first为curr.next=1, second为curr.next.next=2.
3. 我们将curr.next指向second, 此时ListNode变为: 0->2->3->4 1.
4. 我们再将first.next=second.next, 此时ListNode变为: 0->2 1->3->4.
5. 然后我们再将curr.next.next = first, 这样Listnode变为: 0->2->1->3->4.
6. 最后我们将curr=curr.next.next, 此时curr=3, 再次进行while循环.

具体代码实现如下

## 空间时间复杂度分析:

* **Time Complexity: O(logn)**: n是dummyHead的长度, 这里我们每隔2位数遍历一次dummyHead.
* **Space Complexity: O(n)**: 我们用了一个dummyhead来存储所有的元素.


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