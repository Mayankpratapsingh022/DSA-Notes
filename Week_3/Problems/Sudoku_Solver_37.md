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
def print_board(board):
    for row in board:
        print(" ".join(row))
    print()

def isValid(board, row, col, c):
    for i in range(9):  # Check each row and column, and the 3x3 sub-grid for validity
        if board[i][col] == c:  # Check if the number is already in the column
            return False
        if board[row][i] == c:  # Check if the number is already in the row
            return False
        # Check if the number is in the 3x3 sub-grid
        if board[3 * (row // 3) + i // 3][3 * (col // 3) + i % 3] == c:
            return False
    return True  # The number is valid if it is not found in the row, column, or sub-grid

def solveSudoku(board):
    for i in range(len(board)):  # Iterate over each cell in the board
        for j in range(len(board[0])):
            if board[i][j] == '.':  # Find an empty cell
                for c in '123456789':  # Try placing numbers 1 to 9
                    if isValid(board, i, j, c):  # Check if the number can be placed
                        board[i][j] = c  # Place the number
                        print_board(board)  # Print the board for visualization
                        if solveSudoku(board):  # Recursively solve the rest of the board
                            return True  # If solved, return true
                        else:
                            board[i][j] = '.'  # Backtrack by removing the number
                            print_board(board)  # Print the board for visualization
                return False  # Return false if no valid number can be placed
    return True  # Return true if the board is fully solved

# Example board
board = [
    ["5","3",".",".","7",".",".",".","."],
    ["6",".",".","1","9","5",".",".","."],
    [".","9","8",".",".",".",".","6","."],
    ["8",".",".",".","6",".",".",".","3"],
    ["4",".",".","8",".","3",".",".","1"],
    ["7",".",".",".","2",".",".",".","6"],
    [".","6",".",".",".",".","2","8","."],
    [".",".",".","4","1","9",".",".","5"],
    [".",".",".",".","8",".",".","7","9"]
]

solveSudoku(board)
```

### Explanation of Code

1. **print_board Function:** Prints the current state of the board in a readable format.
2. **isValid Function:** Checks if placing a number `c` in cell `(row, col)` is valid:
   - Checks the entire column to ensure `c` is not already present.
   - Checks the entire row to ensure `c` is not already present.
   - Checks the 3x3 sub-grid to ensure `c` is not already present.
3. **solveSudoku Function:** Solves the Sudoku using backtracking:
   - Iterates over each cell in the board.
   - If an empty cell is found, tries placing numbers from 1 to 9.
   - For each number, checks if it is valid using the `isValid` function.
   - If valid, places the number and prints the board.
   - Recursively calls `solveSudoku` to solve the rest of the board.
   - If placing the number does not lead to a solution, backtracks by removing the number and prints the board.
   - This process continues until the board is fully solved or all possibilities are exhausted.

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
