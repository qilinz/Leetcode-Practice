# Day 7-9 : Breadth-First Search / Depth-First Search
### [Depth-first search (DFS) algorithm](https://en.wikipedia.org/wiki/Depth-first_search)

 DFS is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking.

Main Applications:
- find connected components
- solve puzzles with only one solution, such as mazes.

![Alt Text](https://github.com/qilinz/Leetcode-Practice/blob/main/Study-Plan/images/440px-Depth-First-Search.gif?raw=true)



### [Breadth-first search (BFS) algorithm](https://en.wikipedia.org/wiki/Breadth-first_search)

BFS is an algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and **explores all nodes at the present depth PRIOR to moving on to the nodes at the next depth level**.

Main Applications:
- find connected components
- chess engine
- find the shortest path

![Alt Text](https://github.com/qilinz/Leetcode-Practice/blob/main/Study-Plan/images/Animated_BFS.gif?raw=true)

### [BFS vs DFS](https://www.geeksforgeeks.org/difference-between-bfs-and-dfs/)

## 733. Flood Fill
### Question
An image is represented by an `m x n` integer grid image where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `newColor`. You should perform a flood fill on the image starting from the pixel `image[sr][sc]`.

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `newColor`.

Return the modified image after performing the flood fill.

### Solution
```
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        # get the length of rows and columns
        R = len(image)
        C = len(image[0])
        
        # get the current color of the starting pixel
        color = image[sr][sc]
        
        # if the color does not change, return current image
        if color == newColor:
            return image
        
        # flood fill
        def dfs(r, c):
            # if it's the same color as the starting pixel
            if image[r][c] == color:
                # change it to the new color
                image[r][c] = newColor
                # check the 4-directionally neighbours if not out of range 
                if r-1 >= 0: dfs(r-1, c)
                if r+1 < R: dfs(r+1, c)
                if c-1 >= 0: dfs(r, c-1)
                if c+1 < C: dfs(r, c+1)
        dfs(sr,sc)
        return image

```
### Notes
Pay attention to the index range.
## 695. Max Area of Island
### Question
You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value `1` in the island.

Return the maximum area of an island in `grid`. If there is no island, return `0`.


### Solution
``` 
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        # get counts of rows and columns
        R, C = len(grid), len(grid[0])
        
        # record the max
        area = 0
        
        # record checked positions
        visit = set()
        
        # dfs search
        def dfs(r, c):
            # stop if out of range or 0 or visited
            if r < 0 or r >= R or c < 0 or c >= C or grid[r][c] == 0 or (r,c) in visit:
                return 0
                
            # add (r,c) to visit
            visit.add((r,c))
            
            # return the area of the island
            return (1 + dfs(r-1,c) + dfs(r+1,c) + dfs(r, c-1) + dfs(r, c+1))
        
        # loop through every position 
        for i in range(R):
            for j in range(C):
                area = max(area, dfs(i,j))
        
        return area
```


## 617. Merge Two Binary Trees
### Question
You are given two binary trees root1 and root2.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return the merged tree.

Note: The merging process must start from the root nodes of both trees.

### Solution1: modify the one of the given tree
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        # if one tree is empty, return the other
        if root1 is None:
            return root2
        if root2 is None:
            return root1
            
        # add the root2 to root1
        root1.val += root2.val
        root1.left = self.mergeTrees(root1.left, root2.left)
        root1.right = self.mergeTrees(root1.right, root2.right)
        return root1
```
### Solution2: create a new tree 
``` 
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        # if both trees are not empty, add them to new tree "root"
        if root1 and root2:
            root = TreeNode(root1.val + root2.val)
            root.left = self.mergeTrees(root1.left, root2.left)
            root.right = self.mergeTrees(root1.right, root2.right)
            return root
        
        # if any empty tree, return the one that is not empty
        else:
            return root1 or root2
```



## 116. Populating Next Right Pointers in Each Node
### Question
You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.
### Solution
``` 
class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root:
            return root
        head = root
        next_level = root.left
        while next_level:
            next_level.next = head.right
            while head.next:
                head.right.next = head.next.left
                head.next.left.next = head.next.right
                head = head.next
            head = next_level
            next_level = next_level.left
        return root
```
### Solution 2
``` 
class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root:
            return root
        head = root
        next_level = root.left
        while head.left:
            head.left.next = head.right
            if head.next:
                head.right.next = head.next.left
                head = head.next
            else:
                head = next_level
                next_level = next_level.left
        return root
```
### Notes
My question is that which one is more readable?

## 733. Flood Fill
### Question
### Solution
### Notes

## 733. Flood Fill
### Question
### Solution
### Notes