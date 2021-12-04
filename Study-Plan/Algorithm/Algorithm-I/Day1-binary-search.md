# Day 1 - Binary Search

## 704. Binary Search
### Question
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Constraints:**
- 1 <= `nums.length` <= 10<sup>4</sup>
- -10<sup>4</sup> < `nums[i], target` < 10<sup>4</sup>
- All the integers in `nums` are unique.
- `nums` is sorted in ascending order.

### Solution
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        # find the first index and last index        
        low = 0
        high = len(nums) - 1
        
        # if there're still items that have not been searched    
        while low <= high:
            # find the middel index of the list left
            middle = low + (high - low) // 2
                
            if nums[middle] == target:
                return middle
            elif nums[middle] > target:
                high = middle - 1
            else:
                low = middle + 1
        
        return -1
```

### Notes:
1. `high = middle -1` is better than `high = middle`, as item with index middle has been checked.
2. Because of 1, it should be `low <= high` rather than `low < high` (not to miss any item).
3. Regarding exceptions: 
   1. `target` can be higher than the biggest number or lower than the smallest number in the list. 
   2. `target` is within the range, but not in the list. Example: `target = 2` and `list = [1, 3]`.

## 278. First Bad Version
### Question
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Constraints:**
- 1 <= bad <= n <= 2<sup>31</sup> - 1

### Solution
```
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return an integer
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        first = 1
        last = n
        
        while first < last:
            bad = first + (last - first) // 2 
            if not isBadVersion(bad):
                first = bad + 1
            else:
                last = bad
        
        return last
```
### Notes
- We don't care about Good versions, therefore, whenever the middle check is a good version, the next check starts from `first = bad + 1`. 
- We care about Bad versions, therefore, if the middle check is a bad version:
  - Discard the right sides as they cannot be the first bad version. 
  - Keep the middle check as it might be the first bad version.

## 35. Search Insert Position
### Question
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Constraints:**
- 1 <= `nums.length` <= 10<sup>4</sup>
- -10<sup>4</sup> <= `nums[i]` <= 10<sup>4</sup>
- `nums` contains distinct values sorted in ascending order.
- -10<sup>4</sup> <= `target` <= 10<sup>4</sup>

### Solution
```
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) -1
        
        while left <= right:
            middle = left + (right - left) // 2
            
            if nums[middle] == target:
                return middle
            elif nums[middle] > target:
                right = middle - 1
            else:
                left = middle + 1
        
        return left
```

### Notes
- Finally, get the third one right by myself. Congrats to myself! 