# Day 10-11 : Recursion / Backtracking
## 21. Merge Two Sorted Lists
### Question
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.


### Solution
``` 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        # if anyone is None, return
        if not (list1 and list2):
            return list1 or list2
            
        if list1.val > list2.val:
            list2.next = self.mergeTwoLists(list2.next, list1)
            return list2
        else:
            list1.next = self.mergeTwoLists(list1.next, list2)
            return list1
        
```
## 21. Merge Two Sorted Lists
### Question
Given the head of a singly linked list, reverse the list, and return the reversed list.

### Solution: [iterative](https://leetcode.com/problems/reverse-linked-list/discuss/1449712/Easy-C%2B%2BJavaPythonJavaScript-Explained%2BAnimated)
``` 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head
        while cur:
            n = cur.next
            cur.next = prev
            prev = cur
            cur = n
        return prev
```
### Solution: recursive
``` 
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
            
        # find the laat node pf the list
        node = self.reverseList(head.next)
        
        # reverse the pointer
        head.next.next = head
        head.next = None
        return node
```
## 77. Combinations
### Question
Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].

You may return the answer in any order.
### Solution


## 21. Merge Two Sorted Lists
### Question

### Solution

## 21. Merge Two Sorted Lists
### Question

### Solution