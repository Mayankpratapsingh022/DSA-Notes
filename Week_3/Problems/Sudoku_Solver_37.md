### Sudoku Solver Using Backtracking

#### Pseudocode

1. **Find an Empty Cell:**
   - Locate the first empty cell in the Sudoku grid.
2. **Try Possible Numbers:**
   - For each number from 1 to 9, do the following:
3. **Check Validity:**
   - Check if the number can be placed in the cell according to Sudoku rules.
4. **Place Number:**
   - If valid, place the number in the cell.
5. **Recursive Call:**
   - Recursively try to solve the rest of the grid.
6. **Backtrack:**
   - If placing the number does not lead to a solution, remove the number and try the next one.
7. **Continue:**
   - Repeat until the grid is fully solved or no valid placements are possible.
8. **Return Result:**
   - Return true if a solution is found, otherwise false.

### Explanation of Pseudocode

- **Find an Empty Cell:** Identifies the cell in the grid that has not been filled yet (represented by '.').
- **Try Possible Numbers:** Iterates through numbers 1 to 9 and attempts to place them in the empty cell.
- **Check Validity:** Before placing a number, checks whether the number does not violate Sudoku rules (uniqueness in row, column, and 3x3 sub-grid).
- **Place Number:** If the number is valid, places the number in the cell.
- **Recursive Call:** Calls the function recursively to solve the rest of the grid.
- **Backtrack:** If the placement does not work, removes the number and tries the next possible number.
- **Continue:** This process continues until the grid is fully solved or all possibilities are exhausted.
- **Return Result:** Returns true if a solution is found; otherwise, it returns false.

### Python Code for Sudoku Solver with Explanation

```python
from typing import List

class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        # solve function that solves the Sudoku puzzle
        def solve(board):
            # We have to traverse the matrix into rows and columns
            for i in range(len(board)):  # Loop over each row
                for j in range(len(board[0])):  # Loop over each column
                    # Board is empty
                    if board[i][j] == '.':  # Check if the current cell is empty
                        for c in '123456789':  # Try placing numbers 1 to 9 in the cell
                            # Function call which determines the three conditions
                            # 1. Row-wise uniqueness
                            # 2. Column-wise uniqueness
                            # 3. 3x3 sub-boxes uniqueness
                            if isValid(board, i, j, c):  # Check if placing 'c' in board[i][j] is valid
                                board[i][j] = c  # Place 'c' in board[i][j]
                                if solve(board):  # Recursively solve the rest of the board
                                    return True  # If the board is solved, return True
                                else:
                                    # This is where we are backtracking
                                    board[i][j] = '.'  # Remove 'c' from board[i][j] and try the next number
                        return False  # If no number can be placed, return False (trigger backtracking)
            return True  # If the board is fully solved, return True
        
        # Function to check if placing 'c' in board[row][col] is valid
        def isValid(board, row, col, c):
            for i in range(9):  # Loop over each cell in the row, column, and 3x3 sub-box
                if board[i][col] == c:  # Check column for duplicates
                    return False
                if board[row][i] == c:  # Check row for duplicates
                    return False
                if board[3 * (row // 3) + i // 3][3 * (col // 3) + i % 3] == c:  # Check 3x3 sub-box for duplicates
                    return False
            return True  # If no duplicates are found, return True
        
        solve(board)  # Call the solve function to start solving the board
```

### Explanation in Easy Manner (for a Kid)

Imagine you have a big puzzle board with 81 little boxes arranged in a 9x9 grid. Some of these boxes already have numbers from 1 to 9, and some are empty. Your job is to fill in the empty boxes with numbers from 1 to 9 so that:

1. Each row (like a line of boxes going across) has all the numbers from 1 to 9 with no repeats.
2. Each column (like a line of boxes going up and down) has all the numbers from 1 to 9 with no repeats.
3. Each small 3x3 square (like a smaller box inside the big box) also has all the numbers from 1 to 9 with no repeats.

To solve this puzzle, we can use a method called "backtracking." Here's how it works:

1. **Look for an Empty Box:** Start at the first box and look for an empty one.
2. **Try a Number:** Try putting a number from 1 to 9 in the empty box.
3. **Check if it's Okay:** Before you put the number in the box, check three things:
   - Is the number already in the same row?
   - Is the number already in the same column?
   - Is the number already in the same 3x3 square?
4. **Place the Number:** If the number is not in the same row, column, or 3x3 square, put it in the box.
5. **Solve the Next Box:** Move to the next empty box and repeat steps 2-4.
6. **Backtrack if Needed:** If you can't find a number that works, go back to the previous box and try a different number. This is called "backtracking."
7. **Finish the Puzzle:** Keep doing this until all the boxes are filled correctly.

### Simplified Code Explanation (Step-by-Step)

1. **Define Functions:**
   - We create a function called `solve` to go through each box and try to fill it.
   - We create another function called `isValid` to check if a number can go into a specific box without breaking the rules.

2. **Go Through Each Box:**
   - In the `solve` function, we loop through every box in the grid.
   - If a box is empty (represented by '.'), we try putting numbers 1 to 9 in it.

3. **Check the Number:**
   - For each number we try, we use the `isValid` function to check if the number is already in the same row, column, or 3x3 square.

4. **Place and Move On:**
   - If the number is okay to place, we put it in the box and call `solve` again to move to the next box.
   - If we solve the puzzle, we return `True` to indicate success.

5. **Backtrack if Needed:**
   - If placing a number doesn't lead to a solution, we remove it (backtrack) and try the next number.
   - If no numbers work, we return `False` to backtrack to the previous box.

6. **Start Solving:**
   - Finally, we call `solve(board)` to start solving the Sudoku puzzle.

This way, we fill in the Sudoku board step by step, checking and backtracking as needed, until the puzzle is completely solved.


### Visualizing the Board at Each Step

#### Initial Board

| 5 | 3 | . | . | 7 | . | . | . | . |
|---|---|---|---|---|---|---|---|---|
| 6 | . | . | 1 | 9 | 5 | . | . | . |
| . | 9 | 8 | . | . | . | . | 6 | . |
| 8 | . | . | . | 6 | . | . | . | 3 |
| 4 | . | . | 8 | . | 3 | . | . | 1 |
| 7 | . | . | . | 2 | . | . | . | 6 |
| . | 6 | . | . | . | . | 2 | 8 | . |
| . | . | . | 4 | 1 | 9 | . | . | 5 |
| . | . | . | . | 8 | . | . | 7 | 9 |

#### Intermediate Steps
- Let's say we place '1' in the first empty cell (0, 2), then the board looks like:

| 5 | 3 | 1 | . | 7 | . | . | . | . |
|---|---|---|---|---|---|---|---|---|
| 6 | . | . | 1 | 9 | 5 | . | . | . |
| . | 9 | 8 | . | . | . | . | 6 | . |
| 8 | . | . | . | 6 | . | . | . | 3 |
| 4 | . | . | 8 | . | 3 | . | . | 1 |
| 7 | . | . | . | 2 | . | . | . | 6 |
| . | 6 | . | . | . | . | 2 | 8 | . |
| . | . | . | 4 | 1 | 9 | . | . | 5 |
| . | . | . | . | 8 | . | . | 7 | 9 |

- If '1' doesn't lead to a solution, we backtrack and try '2', then the board might look like:

| 5 | 3 | 2 | . | 7 | . | . | . | . |
|---|---|---|---|---|---|---|---|---|
| 6 | . | . | 1 | 9 | 5 | . | . | . |
| . | 9 | 8 | . | . | . | . | 6 | . |
| 8 | . | . | . | 6 | . | . | . | 3 |
| 4 | . | . | 8 | . | 3 | . | . | 1 |
| 7 | . | . | . | 2 | . | . | . | 6 |
| . | 6 | . | . | . | . | 2 | 8 | . |
| . | . | . | 4 | 1 | 9 | . | . | 5 |
| . | . | . | . | 8 | . | . | 7 | 9 |

- This process continues, exploring different possibilities, until the board is fully solved.

### Final Solved Board
| 5 | 3 | 4 | 6 | 7 | 8 | 9 | 1 | 2 |
|---|---|---|---|---|---|---|---|---|
| 6 | 7 | 2 | 1 | 9 | 5 | 3 | 4 | 8 |
| 1 | 9 | 8 | 3 | 4 | 2 | 5 | 6 | 7 |
| 8 | 5 | 9 | 7 | 6 | 1 | 4 | 2 | 3 |
| 4 | 2 | 6 | 8 | 5 | 3 | 7 | 9 | 1 |
| 7 | 1 | 3 | 9 | 2 | 4 | 8 | 5 | 6 |
| 9 | 6 | 1 | 5 | 3 | 7 | 2 | 8 | 4 |
| 2 | 8 | 7 | 4 | 1 | 9 | 6 | 3 | 5 |
| 3 | 4 | 5 | 2 | 8 | 6 | 1 | 7 | 9 |


[Sudoku Solver Leetcode](https://leetcode.com/problems/sudoku-solver/submissions/1326224716/)
