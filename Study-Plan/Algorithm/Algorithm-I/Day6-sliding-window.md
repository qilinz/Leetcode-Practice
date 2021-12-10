# Day 6 : Sliding Window
## 3. Longest Substring Without Repeating Characters
### Question
Given a string s, find the length of the longest substring without repeating characters.

### Solution
``` 
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = 0    # left pointer
        result = 0  # record the length to return
        dic = {}    # creat a dict to store the position of each item
        for right in range(len(s)):  # right pointer
            if s[right] in dic:  
            # when an item is repeated,
                # if the item stored in the dic is on the left of the left pointer, pointer does not move: left = left
                # if it is on the right of the left pointer, the left pointer should move to the item next to it: left = dic[s[right]] + 1
                left = max(dic[s[right]] + 1, left)
                
            result = max(result, right-left+1)
            # record current item
            dic[s[right]] = right
        return result
```

## 567. Permutation in String
### Question
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Constraints:**
- 1 <= s1.length, s2.length <= 104
- s1 and s2 consist of lowercase English letters.

### Solution
``` 
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        list1 = [ord(i) - ord('a') for i in s1]
        list2 = [ord(i) - ord('a') for i in s2]
        check1 = [0] * 26
        check2 = [0] * 26
        # STEP 1: transform s1
        for _ in range(len(list1)):
            check1[list1[_]] += 1
        
        # STEP 2: transform s2 and check with s1
        for _ in range(len(list2)):
            check2[list2[_]] += 1
            if _ >= len(list1):
                check2[list2[_ - len(list1)]] -= 1
            if check1 == check2:
                return True
        return False
```
### Notes
- `ord()` return an integer representing the Unicode character. According to the constraints of the problem, any item in the two string only has 26 possibilities: [a-z]. Using `ord(i) - ord("a")`, [a-z] will be represented by numbers 0-25. 
  - -> `list1` and `list2`
  - e.g. `s1 = ["ab"]` -> `list1 = [0, 1]`
- Next, as it could be a permutation, we need to find ways to check regardless the order. Therefore, new lists containing a pre-defined position are created: a list containing placeholders for any possible character. When a char is checked, the count will be increased by 1. 
  - -> `check1` and `check2`
  - as we don't know `len(s1)` and `len(s2)`, it's better to transform them separately to prevent `IndexError`.
  - Through "STEP 1", `s1` will be represented by `check1` - a list with length of 26 containing counts for each char in `s1`
  - e.g. `check1 = [1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]`
- Then, we transform `s2` using the same strategy and check with s1 through sliding window.
  - count current character in `check2`
  - if current window is longer than `len(s1)`, remove the first count in the window. 
  - check with `check1`