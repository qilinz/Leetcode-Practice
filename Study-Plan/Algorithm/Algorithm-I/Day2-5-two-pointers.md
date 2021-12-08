# Day 2-5 : Two Pointers
Two Pointers mean firstly checking two elements - the first and the last elements in the array, and then check the first and the last elements in the array that have not been checked, so on and so force. It's a technique typically used in **searching pairs in a sorted array**.
## 977. Squares of a Sorted Array
### Question
Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Follow up: Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

### Solution
```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        left = 0
        right = n-1
        i = n-1
        new_list = [0] * n
        for i in range(n-1, -1, -1):
            if abs(nums[left]) > abs(nums[right]):
                new_list[i] = nums[left] ** 2
                left += 1
            else:
                new_list[i] = nums[right] ** 2
                right -= 1
        return new_list
```
### Notes
- The above solution is O(n) in complexity.

## 189. Rotate Array
### Question
Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.


Follow up: Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.
Could you do it in-place with `O(1)` extra space?

### Solution
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k % n
        self.reverse(nums, 0, n-1)
        self.reverse(nums, 0, k-1)
        self.reverse(nums, k, n-1)
        
    def reverse(self, nums: List[int], start: int, end: int):
        while start < end:
            temp = nums[start]
            nums[start] = nums[end]
            nums[end] = temp
            start += 1
            end -= 1
```
### Notes
The approach is: (1) reverse all the elements of the array; (2) reverse the first k elements of the array; (3) reverse the rest n-k elements of the array.

Let n = 7 and k = 3
```
- Original List                   : 1 2 3 4 5 6 7
- After reversing all numbers     : 7 6 5 4 3 2 1
- After reversing first k numbers : 5 6 7 4 3 2 1
- After reversing last n-k numbers: 5 6 7 1 2 3 4 
```

## 283. Move Zeroes
### Question
Given an integer array `nums`, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

### Solution
``` 
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i = 0
        for j in range(len(nums)):
            if nums[j] != 0:
                nums[j], nums[i] = nums[i], nums[j]
                i += 1
```
### Notes
The idea is to generate two pointer, one for iterating the list (`j`), the other to store the position of 0 in `nums` (`i`). If `nums[j] != 0`, this item should be passed, thus: (1) switch with the last 0 item; (2) `i += 1` to record the current position of 0. 

## 167. Two Sum II - Input Array Is Sorted
### Question
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

### Solution
``` 
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers) - 1
        while left < right:
            if numbers[left] + numbers[right] == target:
                return [left+1, right+1]
            elif numbers[left] + numbers[right] > target:
                right -= 1
            else:
                left += 1
```

### Notes:
The idea is that:
- `while left < right` to make sure every item is only used once
- check the sum of the min and the max
  - if sum > target, max is too big, thus should not be used 
  - if sum < target, min is too small, thus should not be used

## 344. Reverse String
### Question
Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array `in-place` with `O(1)` extra memory.
### Solution
My solution:
``` 
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left = 0
        right = len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
        
```
Others' solution:
```
class Solution:
    def reverseString(self, s):
        for i in range(len(s)//2): 
            s[i], s[-i-1] = s[-i-1], s[i]
```
### Notes
The ideas of the two solution are the same: swap the left and the right item of the list. While the two pointers are "increasing" in the same speed, we can use one `i` to  represent `left` and `right`.

## 557. Reverse Words in a String III
### Question
Given a string `s`, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

### Solution
``` 
class Solution:
    def reverseWords(self, s: str) -> str:
        new_list = s.split(" ")
        for i in range(len(new_list)):
            new_list[i] = self.reverse(new_list[i]) 
        return " ".join(new_list)

    
    def reverse(self, word: str) -> str:
        word = list(word)
        for i in range(len(word) // 2):
            word[i], word[len(word) - i - 1] = word[len(word) - i - 1], word[i]
        return "".join(word)
```
### Notes
The idea is to separate the str into list of words first. Then reverse every word. Finally, join them together. 

## 876. Middle of the Linked List
### Question
Given the `head` of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.
### Solution 1
``` 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        arr = [head]
        while arr[-1].next:
            arr.append(arr[-1].next)
        return arr[len(arr) // 2]

```
### Solution 2
```
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```
### Notes
- Solution 1: Add all the nodes to an array, then return the middle item of the array.
- Solution 2: Find the target using two pointers. The fast pointer goes twice as fast as the slow pointer.
  - Why not check `fast.next` only? 
  - That will not work as the `fast.next.next` can be `None`. Error will thus arise when checking the next `fast.next`.

## 19. Remove Nth Node From End of List
### Question
Given the `head` of a linked list, remove the n<sup>th</sup> node from the end of the list and return its head.
### Solution
``` 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        slow = fast = head
        # make fast is n ahead of slow
        for i in range(n):
            fast = fast.next
        
        # Hold exception:
        # if fast is none, it means fast reach "the next of the last node". 
        # This means n = the length of the linked list. 
        # n^th node from the end is the first node of the linked list.
        if fast is None:
            return head.next
        
        # make the fast goes to the end, then the slow will be one node before the target node
        while fast.next:
            slow = slow.next
            fast = fast.next
        
        # jump the target node
        slow.next = slow.next.next
        return head
```
### Notes
- [Best explanation](https://leetcode.com/problems/remove-nth-node-from-end-of-list/discuss/1164542/JS-Python-Java-C%2B%2B-or-Easy-Two-Pointer-Solution-w-Explanation)
- Why head is modified: `slow` is a reference of `head`, not a copy of `head`. Thus, if `slow` is changed, `head` is affected as well. ("you are modifying a child node that the `head` is pointing to")