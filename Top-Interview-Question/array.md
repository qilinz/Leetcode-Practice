# Array
## 26. Remove Duplicates from Sorted Array
### Problem
Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.
### Solution
```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0
        
        left = 0
        for right in range(len(nums)):
            if nums[right] > nums[left]:
                left += 1
                nums[right], nums[left] = nums[left], nums[right]
                
        return left+1
```
### Notes
`nums[right], nums[left] = nums[left], nums[right]` can also be replaced by `nums[left] = nums[right]` as we only need to keep the first `k` items of the list to be correct.
