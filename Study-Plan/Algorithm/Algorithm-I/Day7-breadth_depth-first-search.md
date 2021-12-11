# Day 7-9 : Breadth-First Search / Depth-First Search
[Depth-first search (DFS) algorithm](https://en.wikipedia.org/wiki/Depth-first_search).

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
### Notes


## 733. Flood Fill
### Question
### Solution
### Notes


## 733. Flood Fill
### Question
### Solution
### Notes


## 733. Flood Fill
### Question
### Solution
### Notes

## 733. Flood Fill
### Question
### Solution
### Notes