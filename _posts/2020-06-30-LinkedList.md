---
category: data structure
tags: Linked List
---
# LinkedList
## Defination
### Definition for singly-linked list.
```
 class ListNode:
     def __init__(self, val=0, next=None):
         self.val = val
         self.next = next
```
## Basic Examples
### LeetCode206: Reversed Singlely Linked List
Example:
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
  def reverseList(self, head: ListNode, pre = None) -> ListNode:
        # Recursively
        if(not head):
            return pre
        current = head.next
        head.next = pre
        return self.reverseList(current, head)
        #Iteratively
        current = head
        pre = None
        while(current):
            temp = current.next
            current.next = pre
            pre = current
            current = temp
            # cur.next, prev, cur = prev, cur, cur.next
        return pre
```
## Special Example
### LeetCode141: Linked List Cycle
Example 1:            
Input: head = [3,2,0,-4], pos = 1               
Output: true                      
Explanation: There is a cycle in the linked list, where tail connects to the second node.                
```
 def hasCycle(self, head):
    try:
        slow = head
        fast = head.next
        while slow is not fast:
            slow = slow.next
            fast = fast.next.next
        return True
    except:
        return False
#
Use two pointers, walker and runner.
walker moves step by step. runner moves two steps at time.
if the Linked List has a cycle walker and runner will meet at some point.
#
```
