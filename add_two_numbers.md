# Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
```

## First Solution

Iterate two listnodes at same time, if one ListNode has two nodes and the other one only has one node, then we condisder the second one has 0.

Add two values together and if sum >= 0 we set raise to one so the next sum should increase by one. 
 
Runtime: **20 ms**

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) 
    {
    	ListNode result = new ListNode(0);
    	ListNode curr = result;
    	
    	int raise = 0;
    	while(l1 != null || l2 != null)
    	{
    		int x = (l1 != null) ? l1.val : 0;
    		int y = (l2 != null) ? l2.val : 0;
    		
    		int sum = x + y + raise;
    		raise = (sum >= 10) ? 1 : 0;
    		curr.next = new ListNode(sum % 10);
    		curr = curr.next;
    		
    		if (l1 != null)
    			l1 = l1.next;
			
    		if(l2 != null) 
    			l2 = l2.next;
    		
    	}
    	
    	if (raise == 1) {
    		curr.next = new ListNode(raise);
    	}
    		
    	
    	return result.next;
    }
}
```
