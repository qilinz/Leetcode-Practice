# Day 2 - Two Pointers
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