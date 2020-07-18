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

## Solution

这题应该是有其他更好的解法, 我想出的解法其实挺简单的, 用一个priority queue, 然后遍历lists数组中所有的值, 全部放入这个queue中.

这时候所有的数应该是按照从小到大的顺序在queue中排列的.

最后我们遍历这个queue把元素加到一个新的list node中返回就能得到结果了.

## 空间时间复杂度分析:

* **Time Complexity: O(n)**: n是lists的长度, 这里我们遍历了lists数组.
* **Space Complexity: O(n)**: 我们用了一个queue来存储所有的元素.


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
    public ListNode mergeKLists(ListNode[] lists) 
    {
        ListNode dummyHead = new ListNode(0);
        ListNode curr = dummyHead;
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>( (l1, l2) -> l1-l2);
        
        for(ListNode listNode : lists)
        {
            while(listNode != null)
            {
                queue.offer(listNode.val);
                listNode = listNode.next;
            }
        }
        
        while(!queue.isEmpty())
        {
            ListNode listNode = new ListNode(queue.poll());
            curr.next = listNode;
            curr = curr.next;
        }
        
        return dummyHead.next;
    }
}

```