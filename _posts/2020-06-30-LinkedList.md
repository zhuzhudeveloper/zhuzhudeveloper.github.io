---
category: data structure
tags: LinkedList
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
            current.next = pre
            pre = current
            current = current.next
        return pre
```
