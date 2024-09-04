# Number of Island 200

### Problem Explanation

You are given a 2D grid where:
- `"1"` represents land.
- `"0"` represents water.

Your task is to count how many distinct "islands" of land exist in the grid. An island is a group of connected lands, where connection is defined as land cells being adjacent horizontally or vertically (but not diagonally).

### Approach Overview

You can solve this problem using **Depth-First Search (DFS)**. The idea is to treat the grid like a graph, where each cell is a node. When you find a land cell (`"1"`), perform a DFS to visit all connected land cells, marking them as visited (by changing them to `"0"`) to avoid counting the same island multiple times. Every time you initiate a DFS from an unvisited land cell, it counts as a new island.

### Code Explanation Line by Line

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        # Step 1: Get the dimensions of the grid
        m, n = len(grid), len(grid[0])
```
- **m, n = len(grid), len(grid[0])**: Here, `m` represents the number of rows, and `n` represents the number of columns in the grid. This will be used later to keep the DFS within the bounds of the grid.

```python
        # Step 2: Define the DFS function to mark connected lands
        def dfs(i, j):
            # Check if the current position is out of bounds or not a '1'
            if i < 0 or i >= m or j < 0 or j >= n or grid[i][j] != '1':
                return
```
- **if i < 0 or i >= m or j < 0 or j >= n or grid[i][j] != '1'**: This condition ensures that the DFS doesn't go out of the grid bounds, and it also checks that the current cell is still unvisited land (`"1"`). If the cell is out of bounds or already marked (either `"0"` or visited), the DFS stops.

```python
            else:
                # Mark the current land cell as visited by setting it to '0'
                grid[i][j] = '0'
                # Recursively call DFS for all four possible directions (right, down, left, up)
                dfs(i, j + 1)  # right
                dfs(i + 1, j)  # down
                dfs(i, j - 1)  # left
                dfs(i - 1, j)  # up
```
- **grid[i][j] = '0'**: Once we start the DFS from a land cell, we mark it as visited by changing it to `"0"`. This prevents revisiting the same cell.
- The next four lines call `dfs` recursively for the four possible adjacent directions (right, down, left, and up).

```python
        # Step 3: Initialize the island counter
        num_islands = 0
```
- **num_islands = 0**: This is the counter that will keep track of the number of distinct islands found.

```python
        # Step 4: Iterate through every cell in the grid
        for i in range(m):
            for j in range(n):
                # If the current cell is land, start a DFS from there
                if grid[i][j] == '1':
                    num_islands += 1
                    dfs(i, j)
```
- **for i in range(m), for j in range(n)**: This double loop iterates over every cell in the grid.
- **if grid[i][j] == '1'**: When we find a land cell (`"1"`), it means we’ve found a new island.
- **num_islands += 1**: We increment the island counter because we’ve found a new island.
- **dfs(i, j)**: After incrementing the counter, we start a DFS from this cell to mark all connected land cells.

```python
        # Step 5: Return the number of islands found
        return num_islands
```
- **return num_islands**: Finally, after exploring the entire grid, we return the total number of islands found.

### How to Approach the Problem

1. **Initialization**: You start by reading the dimensions of the grid (`m` rows and `n` columns).
2. **DFS Setup**: For each land cell (`"1"`), initiate a DFS to explore the entire connected island.
3. **Marking Cells**: As you explore cells, mark them as visited by changing them to `"0"`.
4. **Counting Islands**: Every time you start a DFS from a new unvisited land cell, increment the island counter.
5. **End Condition**: When you’ve explored the entire grid, return the island counter.

This algorithm has a time complexity of **O(m * n)** because each cell is visited once. It is efficient for grids with up to 300x300 cells.

[Number of Islands Leetcode](https://leetcode.com/problems/number-of-islands/submissions/1378586454/)
